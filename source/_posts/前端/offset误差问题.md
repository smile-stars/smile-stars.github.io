---
title: v-for遍历渲染图片，获取元素的offsetTop不准确
date: 2023-10-13 09:39:18
categories:
	- 前端
tags:
	- 记录
---

## 问题描述

使用v-for渲染包含大量图片的数据时，获取元素的offsetTop不准确，导致无法滚动到指定位置

## 背景

仿照微信聊天页，实现聊天室页面，初始滚动到页面最底部，滚动条到顶部时加载新数据，并将滚动条定位到到前一页数据的顶部。

由于数据中包含大量图片，在通过offsetTop设置滚动条位置时，总是有偏移，图片越多越明显

```javascript
// 每次滚动到最后一条新数据的位置
let scrollTop = document.getElementsByClassName('list-item')[index].offsetTop
document.documentElement.scrollTop = document.body.scrollTop = scrollTop
```

## 分析问题

一般情况下，出现这种问题大多与图片加载有关，Dom渲染后，图片还未加载完成，只是占了一个位置，此时获取到的offsetTop并不包含图片的高度，所以出现问题

## <font color="red">解决方案</font>

### 方案一：固定高度（目前再用）

既然图片未加载完成，offsetTop获取不到图片的高，那么我们给图片加一个盒子，并给盒子固定高度，让图片在盒子里自适应，那么不管图片是否加载完，这一组元素的高度都已经固定了，就能准确获取元素的offsetTop了

> 缺陷：图片尺寸宽高比差异过大，部分图片会出现变形，故需要设置个比较合适的宽高，

```HTML
<div class="media-box opc-0">
	<img v-lazy="item.url+'?x-oss-process=style/thumb'" class="msg-img"  alt="">
</div>

.media-box {
	max-width: xx;
	height: xx;
}
```

### 方案二：结合图片加载方法（待验证）

既然offsetTop受到图片加载的影响，那么我们就在图片加载完成后再获取offsetTop，结合图片的load方法

> 注意：要结合Debounce（防抖）函数使用，避免被重复触发

```HTML
<img src="" @load="imgLoad" >
```

```javascript
this.imgLoad = Debounce(this.imgLoad)

methods: {
	imgLoad () {
		let scrollTop = document.getElementsByClassName('xx').offsetTop
		document.documentElement.scrollTop = document.body.scrollTop = scrollTop
	}
}
```

