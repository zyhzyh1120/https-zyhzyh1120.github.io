---
title: 微信jssdk录音API例子
date: 2020-09-18 19:16:22
tags: 微信
categories: 微信
---

# 微信 jssdk 录音 API 例子

## 首先要引入 jssdk, 可以使用 npm 或者 script 引入

```javascript
// 微信授权 , 需要使用的接口
wxConfig: function (res, jsapiList) {
  wx.config({ //eslint-disable-line
    debug: false, //开启调试模式,调用的所有api的返回值会在客户端alert出来若要查看传入的参数可以在pc端打开参数信息会通过log打出，仅在pc端时才会打印。
    appId: res.data.appid, // 必填，公众号的唯一标识
    timestamp: res.data.timestamp, // 必填，生成签名的时间戳
    nonceStr: res.data.noncestr, // 必填，生成签名的随机串
    signature: res.data.signature,// 必填，签名
    jsApiList: jsapiList // 必填，需要使用的JS接口列表
  });
  wx.ready(function () { //eslint-disable-line
    wx.checkJsApi({ //eslint-disable-line
        jsApiList: jsapiList,
        success: function (res) {
          console.log('checkok', res)
        }
    });
  })
  wx.error(function (res) { //eslint-disable-line
    // debugger
    alert("出错了：" + res.errMsg);
  });
},

// wx录音
audioStart: function () {
  wx.startRecord(); // eslint-disable-line
},

// 点击停止
async audioStop () {
  return new Promise((resolve) => {
    wx.stopRecord({  // eslint-disable-line
      success: function (res) {
          const audioId = res.localId;
          resolve(audioId)
      }
    });
  })
},

// 录制完成, 上传录音
async audioSuccess (id) {
  return new Promise((resolve) => {
    wx.uploadVoice({ // eslint-disable-line
      localId: id, // 需要上传的音频的本地ID，由stopRecord接口获得
      isShowProgressTips: 1, // 默认为1，显示进度提示
      success: function (res) {
          const successId = res.serverId; // 返回音频的服务器端ID
          resolve(successId)
      }
    });
  })
}
```
