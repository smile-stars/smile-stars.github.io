---
title: js常见小问题
date: 2023-09-11 16:18:39
main_color: "#d4a5e7"
tags:
	- javascript
categories:
	- 前端
---

## 一、解构赋值

接口返回数据格式：

```json
{
	"data": {
		"total": 0,
		"list": []
	}
}
```

使用：

`const {list = []} = data.list`

* 问题：当返回的list为`null`时，解构list时设置初始值为`[]`无效

> **原因**：
JavaScript 的解构赋值遵循以下规则：
如果对象的属性存在且不是 undefined，则会使用该属性的值。
如果对象的属性不存在或值是 undefined，则会使用提供的默认值。
因此，当 data.list 的值是 null 时，它会被视为一个有效值，而不是 undefined，所以默认值 [] 不会被应用。

