---
title: 前端八股文-HTML+CSS
tags: 
    - 面试
categories: 
    - 前端
---

该篇文章只要记录前端面试中常见的HTML与CSS面试题目

### 盒模型？标准盒模型+怪异盒模型？

盒模型，顾名思义就是一个盒子，这个盒子由外到内依次是margin->border->padding->content

通过border-sizing可以对标准盒模型与怪异盒模型进行切换

标准盒模型：指的是content+padding+border

怪异盒模型： 指的是content，不包含border与padding



### 块级元素与行内元素的区别？常见的块级元素与行内元素

块元素：独占一行，默认宽度为父元素的宽度，可设置宽高，内外边距
行内元素：宽内为内容宽度，不可设置宽高，可在水平方向上设置padding、margin，垂直方向设置padding、margin无效

### HTML的语义化标签都有哪些

- header
- nav
- section
- article
- aside
- main
- footer

### 伪元素和伪类的区别？

- 作用不同：伪类是一种状态，可以看作是一种选择器，如：hover、foucs、：nth-child；伪元素是一个元素，是通过CSS模拟出来的盒模型。
- 权重不同：伪类 是 10 （类、属性选择器 [type=submit]）；伪元素 是 1 (标签选择器 )

### CSS如何实现垂直居中？
- flex
- position

### CSS常见的选择器？
- ID选择器
- 类选择器
- 标签选择器
- 属性选择器 （p(class="xx") 选中class值为xx的P标签）
- 通配符选择器 *

### CSS选择器的优先级

**!important > id选择器 > class选择器 > 属性选择器 > 标签选择器 > 通配符选择器**

### 长度单位PX、em、rem的区别是什么？

1. PX是基本单位，绝对长度
2. em相对于当前元素的font-size，相对单位
3. rem相对于根元素的font-size

### 关于弹性盒布局

即弹性布局，为盒状模型提供最大的灵活性。 任何一个容器都可以指定为 Flex 布局。

采用flex布局的盒子成为容器，容器中的所欲子元素，自动成为容器成员，称为“项目”

包含两根轴：水平方向的主轴，垂直方向上的交叉轴

设置在容器上的属性：
- flex-direction：指定容器主轴的方向 （row | row-reverse | column | column-reverse;）
- flex-wrap：项目排列在轴线上，如果轴线上排列不下，要如何换行 （nowrap | wrap | wrap-reverse;）
- flex-flow：flex-direction 属性和 flex-wrap 属性的简写形式，默认值为 row nowrap
- justify-content：主轴对齐方式
    - flex-start（默认值）：左对齐
    - flex-end：右对齐
    - center： 居中
    - space-between：两端对齐，项目之间的间隔都相等。
    - space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔 大一倍。
- align-items：交叉轴上对齐方式

- align-content

设置在项目上的属性：
- order：定义项目的排列顺序。数值越小，排列越靠前，默认为 0
- flex-grow：表示在当前元素占多少份
- flex-shrink：子元素的宽度大于父元素宽度时，要收缩的值
- flex-basis：表示 flex中的剩余空间的大小
- flex：flex：1相当于 `flex: flex-grow flex-shrink flex-basis`
- align-self：单独给项目设置交叉轴的对齐方式

### 浮动塌陷问题的解决方法？
1. 给浮动元素的父元素添加高度
2. clear: both | left | rigth
3. 在浮动元素后面添加一个空元素，设置clear：both
4. 给浮动的盒子添加一个伪元素:after，设置clear: both
4. overflow: hidden

### position属性值及其含义
- static: 默认值，没有定位
- fixed：固定定位，相对于浏览器窗口进行定位
- absolute： 绝对定位，相对于第一个有定位的父元素定位
- relative： 相对定位，根据定位元素自身的位置进行定位

### BFC、IFC是什么？

`BFC`：块级格式化上下文，达到隔离的作用，让满足条件的元素内部的子元素不会影响到元素内部。**解决margin塌陷问题**
    每个BFC区域都是独立的，她只包含该上下文中的所有子元素（直接后代），不包含创建了新的BFC区域的子元素的内部元素
    ```html
    <div class="box1" id="bfc1">
        <div class="box2"></div>
        <div class="box3"></div>
        <div class="box4"></div>
        <div class="box5" id=“bfc2”>
            <div class="box6"></div>
            <div class="box7"></div>
        </div>
    </div>
    ```
    用这段代码来举例，#bfc1是一块BFC区域，这块区域包含了box2、box3、box4、box5，同时bfc2又创建了一个新的BFC区域，这块区域只包含box6、box7。而bfc1这块区域并不包含box6、box7
    **⭐️⭐️⭐️BFC触发条件**
    - float
    - overflow： hidden ｜ auto ｜ scroll
    - disply：inline-block ｜ table-cell ｜ table-caption ｜ flex
    - position： absolute ｜ fixed
`IFC`： 行内格式化上下文