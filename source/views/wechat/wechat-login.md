---
title: wechat
date: 2020-09-18 14:48:54
tags: 微信公众号
categories: 微信
---

# 公众号授权登录代码(含跳转关注公众号)

**注意:**

跳转微信公众号页:
https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=MzU5Mzc1Mzk0NQ==&scene=110#wechat_redirect"

_其中\_\_biz 参数是微信公众号的 appid,base64 转码后所得_

## 代码

```JavaScript
// 点击关注
follow() {
	window.location.href = "https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=MzU5Mzc1Mzk0NQ==&scene=110#wechat_redirect";
},

// 点击暂时不关注
ignore() {
	if (sessionStorage.getItem("redirect")) {
		this.$router.replace(sessionStorage.getItem("redirect"));
	} else {
		this.$router.replace("/");
	}
},

// 得到code跟后台换token
author() {
	this.but_show = true; // 有 code 提示正在进入
	this.$axios({
		url: this.$api.login,
		params: {
			code: this.$route.query.code,
			uid: this.uid
		}
	}).then(res => {
		if (res.code == 200) {
			sessionStorage.setItem("token", res.data.token);
			localStorage.setItem("user_img", res.data.avatar);
			localStorage.setItem("user_id", res.data.uid);
			localStorage.setItem("nickname", res.data.nickname);
			localStorage.setItem("is_vip", res.data.is_vip);
			if (res.data.subscribe == 0) {
				this.guideShow = true;
					return;
			}
			this.Ignore();
			}
	});
},

// 初始进入页面 ,获取code
login() {
	this.but_show = true;
	let code = this.$route.query.code;
	if (sessionStorage.getItem("token")) {
		//本地token
		if (sessionStorage.getItem("redirect")) {
			this.but_show = true;
			this.$router.replace({ path: sessionStorage.getItem("redirect") });
		}
	} else if (code) {
			// 有code则进行登录
			this.author();
	} else {
		let r_url = window.location.href.split("?")[0];
		r_url = encodeURIComponent(r_url);
		window.location.href = "https://open.weixin.qq.com/connect/oauth2/authorize?appid=wxid&redirect_uri=" + r_url + "&response_type=code&scope=snsapi_userinfo&state=1#wechat_redirect";
	}
}

```
