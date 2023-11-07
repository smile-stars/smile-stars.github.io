---
title: chrome调试小技巧
date: 2022-08-17 14:05:36
categories: 
    - 前端
---


## 一键重新发起请求

与后台联调或者排查Bug时，听到比较多的话大概就是：**你再重新请求一次**。可能有人会刷新一下页面，当然也会有人这样做：

1. 打开控制台，选中`network`

2. 选择要重新发送的请求

3. 右键选择`Replay XHR`
![小技巧](https://gitee.com/syy1101/image/raw/master/1.png)

快捷地请求需要再次请求的接口，又不用刷新页面，简直爽翻

## 在控制台快速发起请求

有时候针对同样的请求，需要修改入参重新发起请求，有人这样做：

1. 选中network
2. 选择要修改入参的的接口
3. 选择`Copy as fetch`
4. 在控制台粘贴代码，修改入参回车
![小技巧](https://gitee.com/syy1101/image/raw/master/2.png)
![小技巧](https://gitee.com/syy1101/image/raw/master/3.png)

## 复制Javascript变量

假如你的代码输出一个比较复杂的对象，你又想复制下来发送给别人，怎么办？`JSON.stringify()`再复制吗？
有人用copy函数实现：
![小技巧](https://gitee.com/syy1101/image/raw/master/4.png)
直接回车，粘贴到编辑器中长这样：
![小技巧](https://gitee.com/syy1101/image/raw/master/5.png)

## 一键展开所有的DOM元素

调试元素是=时，层级比较深的情况下，有一种更方便的方式去展开进行调试
> 按住opt键，然后点击要展开的最外层元素

展开后效果：
![小技巧](https://gitee.com/syy1101/image/raw/master/6.png)

## "$"与“$$”选择器

 大家估计都控制台用过document.querySelector与document.querySelectAll选择当前页面的元素，不过，这一大串着实长了点，完全可以用$ 与 $$ 替代
 ![小技巧](https://gitee.com/syy1101/image/raw/master/7.png)

 所以，大家更愿意用长串还是俩符号呢

 ## Add conditional breakpoint条件断点

 例如下面的代码，希望动物名称是“dog”时触发断点，可以怎么去操作？
 ``` js
 const animal = [{
     name: "cat",
     color: "red"
 }, {
     name: "dog",
     color: "pink"
 }, {
     name: "monkey",
     color: "green"
 }]

 animal.forEach(item => {
     console.log(item.name, item.color)
 })
 ```
如果没有条件断点，那么在调试大量数据的情况下，是不是要点N次debugger
![小技巧](https://gitee.com/syy1101/image/raw/master/8.png)


## 使用$i直接在控制台安装npm包

有时候使用如dayjs或者lodash的某个API，但是你又不想去官网查，咋整？
有这么一个插件`Console Importer`，可以用来在控制台直接安装npm包

1. 安装插件
2. $i('名称')安装npm包



我还木有这么操作过，感兴趣的可以试试😂

