---
title: npm相关
date: 2022-11-21 18:40:20
tags: NPN
categories: NPM
excerpt: npm、nvm、nrm 配置相关
---

# npm、nvm、nrm 配置相关

## CNPM

```Bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## NVM

```Bash
nvm version   // 当前版本
nvm li    // 列出本地node实例
nvm list available    // 查看可下载node版本列表

nvm install 4.2.2     // 安装
nvm install 4.2       // nvm 会寻找 4.2.x 中最高的版本来安装
nvm install latest    // 下载最新的稳定版node
nvm uninstall 4.2.0   // 卸载node

nvm current		// 查看当前版本
nvm proxy			// 设置代理

nvm use 4.2.2 		// 切换不同版本
nvm use node		// 切换到本地最新
nvm run 4.2.2 --version	// 运行指定的node

nvm which 4.2.2		// 确定指定版本路径

# 注意： 以下为必操作
// 在setting 文件加， 避免node跟npm版本问题、node不带npm问题
node_mirror: https://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/

```

## npm 配置相关

```Bash
# 镜像源链接切换，查看镜像源使用状态
npm get registry
```

```Bash
### 设置镜像源
npm get registry
npm config set registry <url>
```

```Bash
# 安装私有包
# 普通的
# 先安装私有 npm 包：npm install <name> --registry=<url>
# 然后安装公共 npm 包

# 或
  npm --registry https://registry.npm.taobao.org install <name>
```

```bash
# 需要先注册的(例子)
npm set registry http://47.101.202.23:4873/ // 设置
npm adduser --registry http://47.101.202.23:4873/ // 注册
npm login <username> //登录
npm profile set password --registry http://47.101.202.23:4873/
```

```bash
# 安装临时包
npm install express --no-save // 安装临时包, 此次安装不会记录在 package.json
```

## nrm

```bash
使用: nrm <name>
下载: nrm：npm install -g nrm
查看可切换的镜像源： nrm ls
切换淘宝镜像源：nrm use taobao
// (_表示正在使用的镜像源)
_ npm -------- https://registry.npmjs.org/
yarn ------- https://registry.yarnpkg.com/
cnpm ------- http://r.cnpmjs.org/
taobao ----- https://registry.npm.taobao.org/
nj --------- https://registry.nodejitsu.com/
npmMirror -- https://skimdb.npmjs.com/registry/
edunpm ----- http://registry.enpmjs.org/
```

### nrm 中主要的命令提示：

- nrm -V：查看当前 nvm 版本； (即：是 ‘nrm -Version’ 简写)；
- nrm -h：显示所有命令； (即：是 ‘nrm -help’ 简写)；
- nrm current：显示当前源名称;
- nrm use <registry>：切 ‘npm’ 换源;
- nrm add <registry> <url> [home]：添加一个源; (比如：公司自己的私有源)；
- nrm set-auth <registry> <value> [always]：设置自定义源的授权信息；
- nrm set-email <registry> <value>：给自定义源设置路径；
- nrm set-hosted-repo <registry> <value>：设置发布到自定义源的 ‘npm’ 托管仓储
- nrm del <registry>：删除自定义源;
- nrm home <registry> [browser]：浏览器中打开源首页；
- nrm publish [options] [<tarball>|<folder>]：发布包到自定义源，如果没有使用自定义源，则直接发布到 npm；
- nrm test [registry]：测试源的访问速度； 不加 ‘registry’ 时，默认测试所有的源速度；

### 定制源

```bash
# 定制的源()
# 特别适用于添加企业内部的私有源，执行命令 nrm add <registry> <url>，其中 reigstry 为源名，url 为源的路径
添加: nrm add <registry> http://192.168.0.127:8527/repository/npm-public/
移除: nrm del <registry>
测试延迟: nrm test
```

## 代理

```bash
#设置代理
git 设置 #直接代理
git config --global http.proxy http://127.0.0.1:80
git config --global https.proxy https://127.0.0.1:80

#授权代理
git config --global http.proxy http://username:password@127.0.0.1:80
git config --global https.proxy https://username:password@127.0.0.1:80

#取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy

npm 设置 #直接代理
npm config set proxy http://127.0.0.1:80
npm config set https-proxy https://127.0.0.1:80 #授权代理
npm config set proxy http://username:password@127.0.0.1:80
npm config set https-proxy https://username:password@127.0.0.1:80
```

## souceTree 使用问题

### 拉取、提交提示权限问题

```text
 选项 > 一般 > SSH客户端配置 > 把秘钥配置好
```
