---
title: vue2
date: 2023-01-17 14:49:26
---

# Vue.js

### 1. 对于Vue是一套渐进式框架的理解

1.  数据驱动，也叫双向数据绑定vue数据观测在技术上实现，利用的是ES5 Object.defineProperty和储存器的属性：gerter和setter（所以只兼容到IE9及以上版本），可称为基于依赖的收集的观测机制。核心VM，即ViewModel，保证数据和视图的一致性。
2.  组件系统
    模板（template）：模板声明了数据和最终展示给用户的DOM之间的映射关系。
    初始数据（data）：一个组件的初始数据状态。对于可复用的组件来说通常是一个私有的状态。
    接受外部的参数（props）：组件之间通过参数来进行传递跟共享
    方法（methods）：对数据的改动操作一般都在组件的方法中进行
3.  生命周期函数钩子
4.  私有资源（assets）：Vue.js当中将用户自定义指令、过滤器、组件，⼀个组件可以声明⾃⼰的私有资源。私有资源只有该组件和它的⼦组件可以调用。
5.

*   总结： 一是双向数据绑定，二是组件系统，组件系统既是.vue文件当中内容
*   补充 =》 渐进式：没有多做职责之外的事。

### 生命周期

*   创建前 **beforeCreate()**
*   创建后 **created()**
*   挂载前 **beforeMount()**
*   挂载后 **mounted()**
*   更新前 **beforeUpdate()** 该钩子在服务器端渲染期间不被调用
*   更新后 **update()**
*   keep-alive 组件激活 **activated()**
*   销毁前 **beforeDestroy()**
*   销毁后 **destroyed()** 该钩子在服务器端渲染期间不被调用

### Vue几种常用的指令

**v-model、v-if、v-show、v-show、v-hide、v-for、v-bind、v-on、v-model、v-html、v-pre、v-once**

*   v-model 常用于表单组件实现双向数据绑定
*   v-if：根据表达式的值的真假条件渲染元素。在切换时元素及它的数据绑定/组件被销毁和重建
*   v-else v-else-if
*   v-show 显示元素
*   v-hide 隐藏元素
*   v-html 解析html标签
*   v-text 解析文本
*   v-pre：跳过这个元素和它的子元素的编译过程，可以加快编译
*   v-once：只渲染元素和组件一次，随后的重新渲染，元素、组件及其子节点将被视为静态内容并跳过，可用于优化更新性能。
*   v-bind 属性绑定

### Vue常用的修饰符

*   **v-on** 指令常用修饰符:
    *   **.stop** : 调用event.stopPropagetion(), 禁止事件冒泡
    *   **.prevent** : 调用event.preventDefault() , 阻止事件默认行为
    *   **.self** : 只当事件是从绑定的元素本身触发时才触发回调
    *   **.native** : 监听组件根元素的原生事件

v-bind 指令常用修饰符
.prop :
.sync(2.3.0+) 语法糖 : 会扩展成⼀个更新父组件绑定值的 v-on侦听器

### v-model 指令常用修饰符:

### v-if 和 v-show 的区别

###### 共同点：

&#x9;都是动态显示DOM元素

###### 区别：

&#x9;v-if 是真正的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和⼦组件适当地被销毁和重建；
&#x9;v-show 的元素始终会被渲染并保留在 DOM 中。只是简单地切换元素的css属性display。

&#x9;v-if适合运行条件很少改变时使用，v-show适合频繁切换。

## 父子组件的生命周期

```js
父beforeCreate => 父created => 父beforeMount => 子beforeCreate => 子create => 子beforeMount => 子mounted => 父mounted
```

***

# vue-router

### 完整的 vue-router 导航解析流程

1.  导航被触发。
2.  在失活的组件⾥调⽤离开守卫。
3.  调⽤全局的 beforeEach 守卫。
4.  在重⽤的组件⾥调⽤ beforeRouteUpdate 守卫 (2.2+)。
5.  在路由配置⾥调⽤ beforeEnter。
6.  解析异步路由组件。
7.  在被激活的组件⾥调⽤ beforeRouteEnter。
8.  调⽤全局的 beforeResole 守卫 (2.5+)。
9.  导航被确认。
10. 调⽤全局的 afterEach 钩⼦。
11. 触发 DOM 更新。
12. ⽤创建好的实例调⽤ beforeRouteEnter 守卫中传给 next 的回调函数

### vue-router有哪⼏种导航钩⼦（ 导航守卫 ）

1.  全局守卫： **router.beforeEach**
2.  全局解析守卫： **router.beforeResolve**
3.  局后置钩⼦： **router.afterEach**
4.  路由独享的守卫： **beforeEnter**
5.  组件内的守卫： **beforeRouteEnter、beforeRouteUpdate(2.2 新增)、beforeRouteLeave**

***

# vuex

### 1.概念

*   Vuex是一个专门为vue.js应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态是一种可预测的方式发生发改变。

### Vuex属性

*   **state** - Vuex store实例的根状态对象，用于定义共享的状态变量。
*   **Actions** - 动作，向store发出调用通知。
*   **Mutations** - 修改器， 它用于修改state中定义的状态变量。
*   **Getter** - 获取器， 外部程序通过它获取变量的具体值。或者在取值之前做一些计算（可看做Vuex的计算属性）
*

### 使用

1.  vuex⽂件夹下store.js

```js
import Vue from 'vue'
import Vuex from 'vuex'

//引⼊不同模块需要的共享变量：
import index from './modules/index'

//使⽤vuex
Vue.use(Vuex)

//对外暴露
export default new Vuex.Store({
    modules: {
        index
    }
})
```

1.  vuex⽂件夹下 modelus⽂件夹下 index.js:

```js
//引⼊⼀个常量，保证 action 和 mutations 的统⼀。
import * as types from '../types'
/**
 * App通⽤配置
 */
const state = {
//vuex初始化值
    count : 0
}

const actions = {
    increment({ commit }, n){
        commit(types.TEST_INCREMENT, n)
    },
    decrement({ commit }, state){
        commit(types.TEST_DEREMENT, state)
    }
}
const getters = {
    count: state => state.count
}
const mutations = {
    [types.TEST_INCREMENT](state, n) {
        console.log(n);
        state.count = state.count + 5 + n
    },
    [types.TEST_DEREMENT](state, status) {
        state.count = state.count - 3
    }
}
export default {
 state,
 actions,
 getters,
 mutations
}
```

1.  vuex⽂件夹下type.js:

```js
//暴露常量
export const TEST_INCREMENT = 'TEST_INCREMENT';
export const TEST_DEREMENT = 'TEST_DEREMENT';
```
