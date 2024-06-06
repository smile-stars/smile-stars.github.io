---
title: vue-cliboard2异步操作中使用iOS中失效
date: 2024-06-06 09:18:04
main_color: "#c0e0e0"
tags:
	- 记录
---

- 问题描述：

在iOS中，在异步操作中使用vue-clipboard2实现复制功能，提示复制成功，但未复制到任何内容


- 解决方案：

vue-clipboard2的this.$copyText不能写在异步方法中，所以，可以换种实现方式，或者是给this.$copyText方法包裹一层setTimeout方法，如下：

```javascript
setTimeout(() => {
	this.$copyText('要复制的内容').then(res => {
		console.log('复制成功')
	})
}, 100)
```