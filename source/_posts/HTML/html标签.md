---
title: html标签
date: 2023-03-10 16:29:12
tags:
    - html
categories:
    - 前端
---
原文链接：https://note.noxussj.top/?source=nowcoder

## 基础标签

### div 块元素

介绍：没有任何含义，主要用于 div 进行模块布局

类型：块级元素 block，盒子占用宽度为一整行

属性：没有属性

```html
<div>我是模块</div>
```

### span 行内文本元素

介绍：没有任何含义，主要用于展示文本内容

类型：内联元素 inline，盒子占用宽度根据内容决定

属性：没有属性

```html
<span>我是内容</span>
```

### p 段落元素

介绍：默认自带了 margin 样式，主要用于展示一段内容

类型：块级元素 block，独占一行

属性：没有属性

```html
<p>我是第一行内容</p>
<p>我是第二行内容</p>
```

### img 图片元素

介绍：单标签、主要用于展示图片

类型：内联元素 inline，占用位置根据图片宽度决定

属性： 

- src ：图片的路径
- alt ：图片加载不出来时显示的文本
- width ：图片展示宽度
- height ：图片展示高度

```html
<img src="https://noxussj.top/head.png" alt="加载失败" width="100px" height="100px" />
```

### h1 ~ h6 一级标题 ~ 六级标题

介绍：默认自带了 margin 和 font 样式，主要用于展示不同级别标题

类型：块级元素 block，盒子占用宽度为一整行

属性：没有属性

```html
<h1>我是标题1</h1>
<h2>我是标题2</h2>
<h3>我是标题3</h3>
<h4>我是标题4</h4>
<h5>我是标题5</h5>
<h6>我是标题6</h6>
```

### a 超链接

介绍：默认自带了 font 样式，主要用于展示超链接文字

类型：内联元素 inline，盒子占用宽度根据内容决定

属性：

- href ：超链接地址
- target ：窗口打开方式，_blank（新窗口）、_self（当前窗口，默认）

```html
<a href="http://www.baidu.com" target="_blank">点我跳转</a>
```

### table 表格元素

介绍：一般需要结合 thead、tbody、tr、th、td 标签进行使用，主要用于展示表格

类型：表格元素 table，盒子占用宽度为一整行

属性：

- border ：表格边框
- cellspacing ：每一行之间以及每一列之间的间距
- cellpadding ：每一列的内边距
- width ：表格宽度，不设置则由内容撑开

子元素：

- thead：表头部分
- tbody：表主体部分
- tr：每一行
- th：表头中每一列
- td：表主体中每一列

```html
<table border="1" cellspacing="0" cellpadding="0" width="auto">
    <thead>
        <tr>
            <th>姓名</th>
            <th>年龄</th>
            <th>性别</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>xiaoming</td>
            <td>12</td>
            <td>男</td>
        </tr>
        <tr>
            <td>anqila</td>
            <td>16</td>
            <td>女</td>
        </tr>
    </tbody>
</table>
```
### ul、li 无序列表

介绍：ul 默认自带了 margin、padding 样式，一般需要结合 li 使用，主要用于展示没有序号的列表

类型：块级元素 block，盒子占用宽度为一整行

属性：没有属性

```html
<ul>
    <li>xiaoming</li>
    <li>libai</li>
    <li>anqila</li>
</ul>
```

### ol、li 有序列表

```html
<ol>
    <li>xiaoming</li>
    <li>libai</li>
    <li>anqila</li>
</ol>
```

## 表单标签

### input 输入框

介绍：单标签、默认自带了 margin、width 样式，主要用于展示输入框

类型：行内块级元素 inline-block，盒子占用宽度根据内容决定

属性：

- type：输入框类型
  - text：文本框
  - password：密码框
  - radio：单选框
  - checkbox：多选框
  - button：按钮
  - file：上传文件
- value：表单值

```html
<p>
    <input type="text" placeholder="请输入内容" />
</p>
<p>
    <input type="password" placeholder="请输入密码" />
</p>
<p>
    <span>男<input type="radio" name="gender" value="1" /></span>
    <span>女<input type="radio" name="gender" value="2" /></span>
</p>
<p>
    <span>男<input type="checkbox" name="gender" value="1" /></span>
    <span>女<input type="checkbox" name="gender" value="2" /></span>
</p>
<p>
    <input type="button" value="我是按钮" />
</p>
<p>
    <input type="file" />
</p>
```

### textarea 文本域

介绍：默认自带了 padding、border、width 样式，主要用于展示多行文本输入框

类型：行内块级元素 inline-block，盒子占用宽度根据内容决定

属性：

- rows：行数
- cols：列数
- placeholder：提示信息

```html
<textarea cols="30" rows="2" placeholder="请输入内容"></textarea>
```

### button 按钮

介绍：默认自带了 padding、border 样式，主要用于展示按钮

类型：行内块级元素 inline-block，盒子占用宽度根据内容决定

属性：没有属性

```html
<button>我是按钮</button>
```

### select、option 下拉框

介绍：默认自带了 border 样式，一般需要结合 option 使用，主要用于展示下拉框

类型：行内块级元素 inline-block，盒子占用宽度根据内容决定

属性：

- label：选项文本
- value：选项值

```html

<select>
    <option label="xiaoming" value="a"></option>
    <option label="libai" value="b"></option>
    <option label="anqila" value="c"></option>
</select>
```

## 多媒体标签

### canvas 绘图

在 HTML5 中提供了 canvasAPI ，允许在 canvas 画布上绘制图形

ie6、7、8 不兼容

```html
<canvas width="300" height="300" id="myCanvas"></canvas>

<script>
    var canvas = document.getElementById('myCanvas')
    var context = canvas.getContext('2d')

    context.moveTo(0, 0) // 绘制第一个点，坐标是（0, 0）
    context.lineTo(300, 300) // 绘制第二个点，然后连线，坐标是（300, 300）

    context.lineWidth = 5 // 线条宽度
    context.strokeStyle = '#058' // 线条颜色
    context.stroke() // 开始绘制
</script>
```

### svg、path 矢量图形

介绍：默认自带了 width、height 样式，一般需要结合 path 使用，主要用于展示矢量图形

类型：内联元素 inline，占用位置根据矢量图形宽度决定

属性：

- d：矢量图形路径

```html
<svg viewBox="0 0 1024 1024" width="200" height="200">
    <path
        d="M768 768a32 32 0 0 1 0 64H256a32 32 0 0 1 0-64h512zM512 192a32 32 0 0 1 32 32v345.504l128.64-128.608a32 32 0 0 1 42.496-2.496l2.784 2.496a32 32 0 0 1 2.496 42.464l-2.496 2.784-181.024 181.024a32 32 0 0 1-42.464 2.496l-2.784-2.496-181.024-181.024a32 32 0 0 1 42.464-47.744l2.784 2.496L480 565.024V224a32 32 0 0 1 32-32z"
    ></path>
</svg>
```

### audio 音频

介绍：主要用于展示音频播放器

属性：

- src：音频地址，一般使用 mp3 格式
- loop：是否循环播放
- muted：静音
- autoplay：自动播放，浏览器一般都是禁止的，需要结合静音使用才能生效
- controls：展示播放器控件，样式根据浏览器决定
```html
<audio src="https://noxussj.top/huxiyouhai.mp3" controls></audio>
```

### video 视频

介绍：主要用于展示视频播放器

属性：

- src：视频地址，一般使用 mp4 格式
- loop：是否循环播放
- muted：静音
- autoplay：自动播放，浏览器一般都是禁止的，需要结合静音使用才能生效
- controls：展示播放器控件，样式根据浏览器决定

```html
<video src="https://noxussj.top/oceans.mp4" controls></video>
```

最全面的前端笔记来啦，包含了入门到入行的笔记，还支持实时效果预览。小伙伴们不需要再花时间去写笔记，或者是去网上找笔记了。面试高频提问和你想要的笔记都帮你写好了。支持移动端和 PC 端阅读，深色和浅色模式。

原文链接：https://note.noxussj.top/?source=nowcoder
