---
title: uni-app入门
date: 2023-02-26 19:08:35
tags:
    - uni-app
categories: 
    - 前端
---

### 生命周期
> [官方文档入口](https://uniapp.dcloud.net.cn/)

1. 页面生命周期

`onLoad`：监听页面加载，其参数为上个页面传递的数据，参数类型为 Object（用于页面传参）
`onShow`：监听页面显示。页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面
`onReady`：监听页面初次渲染完成。注意如果渲染速度快，会在页面进入动画完成前触发
`onHide`：监听页面隐藏
`onPullDownRefresh`：监听用户下拉动作，一般用于下拉刷新
`onReachBottom`：页面滚动到底部的事件（不是scroll-view滚到底），常用于下拉下一页数据。具体见下方注意事项

2. 组件生命周期

`beforeCreate`：在实例初始化之前被调用
`created`：实例被创建之后调用
`beforeMount`：在挂载开始之前被调用
`mounted`：挂载到实例上去之后调用。
`beforeUpdate`：数据更新时调用
`updated`：由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子
`beforeDestroy`：实例销毁之前调用
`destoryed`：实例销毁后调用


### 页面调用接口

1. getApp()
`getApp()`函数用于获取当前应用实例，一般用于获取globalData

```js
const app = getApp()

console.log(app.globalData)
```
**注意**
- 不要在定义于 App() 内的函数中，或调用 App 前调用 getApp() ，可以通过 this.$scope 获取对应的app实例
- 通过 getApp() 获取实例之后，不要私自调用生命周期函数。
- 当在首页nvue中使用getApp()不一定可以获取真正的App对象。对此提供了const app = getApp({allowDefault: true})用来获取原始的App对象，可以用来在首页对globalData等初始化

2. getCurrentPages

`getCurrentPages`函数用于获取当前页面栈的实例，以数组形式按栈的顺序给出，第一个元素为首页，最后一个元素为当前页面
**注意**：
`getCurrentPage()`仅用于展示页面栈的情况，请勿修改页面栈，以免造成页面状态错误

### 页面通信

1. uni.$emit(eventName, OBJECT)

触发全局的自定义事件。附加参数都会传给监听器回调

`uni.$emit('update', {msg: '页面更新'})`

2. uni.$on(eventName, callback)

监听全局的自定义事件。事件可以由`uni.$emit`触发，回调函数会接收所有传入事件穿法函数的额外参数

```js
uni.$on('update', function(data) {
    console.log('监听事件来自update，携带参数msg为：' + data.msg)
})
```

3. uni.$off([eventname, callback])

移除全局自定义事件监听器

**Tips：**
- 如果没有提供参数，则移除所有的事件监听器
- 如果只提供了事件，则移除该事件所有的监听器
- 如果同时提供了事件与回调，则只移除这个回调的监听器
- 提供的回调必须跟`$on`的回调为同一个才能移除这个回调的监听器