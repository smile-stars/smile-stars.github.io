---
title: 前端八股文-Vue
date: 2023-02-19 23:11:44
tags: 
    - 面试
categories: 
    - 前端
---

### Vue双向绑定原理？
采用Object.defineProperty对数据进行劫持，编译时，对于用到data中数据的地方创建一个watcher来监听数据变化，然后结合发布订阅模式，在数据变动时发布消息给订阅者，从而触发响应我的回调更新视图

### Vuex的使用方法？

Vuex的数据流是组件中触发action，action提交mutations，mutations修改states。 组件根据 states或getters来渲染页面。

Vuex是个状态管理器。

### MVVM与MVC的区别？

MVVM即Model-View-ViewModel的简写。即模型-视图-视图模型。
模型（Model）指的是后端传递的数据。
视图(View)指的是所看到的页面。
视图模型(ViewModel)是mvvm模式的核心，它是连接view和model的桥梁。

MVC是Model-View- Controller的简写。即模型-视图-控制器。
M和V指的意思和MVVM中的M和V意思一样。
C即Controller指的是页面业务逻辑。
使用MVC的目的就是将M和V的代码分离。
MVC是单向通信。也就是View跟Model，必须通过Controller来承上启下

### Vue组件间通信方式？

### computed与watch的区别？

1. 应用场景不同
    computed用在根据已有属性或者值计算得到新值的情况
    watch用在监听已有值的变化
2. 执行过程不同
    computed所依赖的值没有发生变化，不会重新进行计算，而是等到访问的时候再判断（有缓存）
    watch所依赖的值发生变化后就会执行watch的会调

### v-for与v-if同时使用有什么问题？

### 前端路由原理。比较一下history与hash两种路由
默认hash模式，路径上会有#

原理：
    1. 可以修改url，但不会引起刷新，从而在不刷新的页面的情况下跳转路由。
    2. 监听url改变，根据url渲染对应组件

hash是通过浏览器提供的location API修改url，通过onhashchange方法监听hash改变

history通过浏览器提供的history.pushState或者history.replacestate修改url，通过popState事件监听url改变

### Vue的虚拟Dom，原理？好处？对比手动操作Dom？

### Vue的keep-alive使用以及原理

### Vue 父子组件生命周期的触发顺序

1. 加载渲染过程
    父beforeCreate-》父created-》父beforeMount-》子beforeCreate-》子created-》子beforeMount-》子mounted-》父mounted

2. 更新过程
    父beforeUpdate-》子beforeUpdate-》子updated-》父updated

3. 销毁过程
    父beforeDistory-》子beforeDistory-》子distoryed-》父distoryed

### Vue.nextTick的实现？

### Vue的diff算法

### Vue中key的作用？

### Vue2与Vue3的区别？

### Vue3带来的改变？

### Vue3响应式原理？

### Vue3 新特性

### Pinia是什么？好处？

### 
