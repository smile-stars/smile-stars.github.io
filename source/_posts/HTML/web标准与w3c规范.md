---
title: web标准与w3c规范
date: 2023-03-10 16:05:14
tags:
    - html
categories:
    - 前端
---

原文链接：https://note.noxussj.top/?source=nowcoder

## Web 标准

web 标准主要分为结构、表现、行为 3 部分。

- 结构：指我们平时在 body 里面写的标签，主要是由 html 标签组成
- 表现：指更加丰富 html 标签样式，主要由 css 样式组成
- 行为：指页面和用户的交互，主要由 javascript 部分组成

## W3C 规范

w3c 对 web 标准提出了规范化的要求，即代码规范。

### 对结构的要求

#### 标签字母要小写

正确示范

```html
<div></div>
```

错误示范

```html
<DIV></DIV>
```

#### 标签要闭合

正确示范

```html
<div></div>
<img src="" alt="" />
```
错误示范

```html
<div>
<img src="" alt="">
```

#### 标签不允许随意嵌套

正确示范

```html
<div>
    <i></i>
</div>
```
错误示范

```html
<div>
    <i>
</div>
    </i>
```

### 对表现和行为的要求

建议使用外链 css 和 javascript 脚本，实现结构与表现分离、结构与行为分离，能提高页面的渲染效率，更快地显示网页内容。

最全面的前端笔记来啦，包含了入门到入行的笔记，还支持实时效果预览。小伙伴们不需要再花时间去写笔记，或者是去网上找笔记了。面试高频提问和你想要的笔记都帮你写好了。支持移动端和 PC 端阅读，深色和浅色模式。

原文链接：https://note.noxussj.top/?source=nowcoder
