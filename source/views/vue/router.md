---
title: require.context(自动加载js模块等作用)
date: 2022-12-21 23:21:10
tags: router
categories: vue-router
excerpt: vue-router
---

## vue-router

**使用的简单记录，备忘。**

### 路由懒加载
vue 作为单页面应用, 如果不采用按需加载的方式, 首屏加载是非常慢的,即使做了 loading 也是严重影响用户体验，所以按需加载路由是一个项目的基础构建。(首屏加载优化...后续会记录)，下面是两个目前常用的方法

> 使用require

```js
// router.js
// 一个组件生成一个js文件
{
  path: '/',
  name: 'Index',
  component: resolve => require(['@/view/index'], resolve)
},{
  path: '/my',
  name: 'My',
  component: resolve => require(['@/view/my/index'], resolve)
},{
  path: '/setting',
  name: 'Setting',
  component: resolve => require(['@/view/setting/index'], resolve)
}
```

> 使用 import

```js
// router.js
// 可以指定 webpackChunkName (如下列 /* webpackChunkName: 'Setting ' */, 则会打包为一个模块文件),
// 不指定则单独打包为一个js文件
const Index = () => import("@/view/index");
const My = () => import("@/view/my/index");
const Setting = () =>
  import(/* webpackChunkName: 'Setting ' */ "@/view/setting/index ");
const SettingAbout = () =>
  import(/* webpackChunkName: 'Setting ' */ "@/view/setting/about ");
```

```js
// build/webpack.base.conf.js
// 在 build/webpack.base.conf.js 下的output属性，新增 chunkFilename属性
output: {
 filename: '[name].js',
 //新增chunFilename属性
 chunkFilename: '[name].js'
}
```

---

### vue-router与 webpack的 process.env.NODE_ENV 拓展使用
**开发环境不使用懒加载, 因为懒加载页面太多的话会造成webpack热更新太慢, 所以只有生产环境使用懒加载**

```js
// import-production.js
module.exports = file => () => import('@/views/' + file + '.vue')
```
```js
// import-development.js
module.exports = file => require('@/views/' + file + '.vue').default
```

```js
// router.js
const _import = require('./import-' + process.env.NODE_ENV)

// 全局路由(无需嵌套上左右整体布局)
const globalRoutes = [
  { path: '/404', component: _import('common/404'), name: '404', meta: { title: '404未找到' } },
  { path: '/login', component: _import('common/login'), name: 'login', meta: { title: '登录' } }
]

// 主入口路由(需嵌套上左右整体布局)
const mainRoutes = {
  path: '/',
  component: _import('main'),
  name: 'main',
  redirect: { name: 'home' },
  meta: { title: '主入口整体布局' },
  children: [
    // 通过meta对象设置路由展示方式
    // 1. isTab: 是否通过tab展示内容, true: 是, false: 否
    // 2. iframeUrl: 是否通过iframe嵌套展示内容, '以http[s]://开头': 是, '': 否
    // 提示: 如需要通过iframe嵌套展示内容, 但不通过tab打开, 请自行创建组件使用iframe处理!
    { path: '/home', component: _import('common/home'), name: 'home', meta: { title: '首页' } },
    { path: '/prodInfo', component: _import('modules/prod/prodInfo'), name: 'prodInfo', meta: { title: '产品详情' } }
  ],
  beforeEnter (to, from, next) {
    let authorization = Vue.cookie.get('Authorization')
    if (!authorization || !/\S/.test(authorization)) {
      clearUserInfo(); // 清除登录信息
      next({ name: 'login' });
    }
    next()
  }
}

const router = new Router({
  mode: 'hash',
  scrollBehavior: () => ({ y: 0 }),
  isAddDynamicMenuRoutes: false, // 是否已经添加动态(菜单)路由
  routes: globalRoutes.concat(mainRoutes)
})
```