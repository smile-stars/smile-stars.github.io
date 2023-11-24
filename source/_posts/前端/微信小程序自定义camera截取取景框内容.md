---
title: 微信小程序自定义camera截取取景框内容
date: 2023-11-24 14:13:39
main_color: "#d4a5e7"
tags:
	- 微信小程序
categories:
	- 前端
---

## 问题描述

最近在写需求的时候遇到上传身份证的功能，要求小程序内调起相机显示取景框，并且最终只获取取景框里的内容
![问题描述](https://gitee.com/syy1101/image/raw/master/20231124-1.jpg)

参考：https://blog.csdn.net/zhazhashuai1999/article/details/120201389

## 思路

- 小程序`wx.chooseImage`默认是没有取景框的限制的，又不支持自定义样式，所以需要自定义`camera`组件
- `camera`可以自定义样式，但是默认拍摄的内容是全屏的，所以单独使用`camera`也是不行
- 如果`camera`跟`canvas`一起使用呢？`camera`负责拍摄，`canvas`负责截取指定区域生成图片

## 实践

#### 1、使用camera获取相机

```html
<view class="container">
    <block>
        <camera class='camera' device-position='{{ position }}' binderror='error' bindstop='cancel'></camera>
        <!-- 取景框 -->
        <cover-view class="line">
        </cover-view>
        <cover-view class='btnBox'>
            <cover-view class='cancel' bindtap='cancel'>取消</cover-view>
            <cover-view class='take' bindtap='takePhoto'>
                <cover-view class='round'></cover-view>
            </cover-view>
            <cover-image src='https://hbrand.oss-cn-hangzhou.aliyuncs.com/hzhuihe/lens.png' bindtap='transLens' class='lens'></cover-image>
        </cover-view>
    </block>
    <!-- canvas透明度设为0 !!!-->
    <view class="canvas-box>
        <canvas type="2d" id="myCanvas"></canvas>
    </view>
</view>
```

#### 2、点击“拍照”，调用`takePhoto`拍摄照片并获取临时路径

```javascript
takePhoto () {
        const ctx = wx.createCameraContext()
        ctx.takePhoto({
            quality: 'high',
            success: (res) => {
                this.setData({
                    iPath: res.tempImagePath
                })
            }
        })
    }
```

#### 3、获取canvas实例,传给自定义函数init()

```javascript
takePhoto() {
    const ctx = wx.createCameraContext()
    ctx.takePhoto({
      quality: 'high',
      success: (res) => {
        console.log(res.tempImagePath)

        this.setData({
          iPath: res.tempImagePath
        })
        wx.createSelectorQuery()
          .select('#mycanvas')
          .fields({
            node: true,
            size: true
          }, (res) => {
            const canvas = res.node
            const ctx2 = canvas.getContext('2d');
            this.init(ctx2, canvas)
          })
          .exec()
      },
      fail: (err) => {
        console.log(err)
      }
    })
  }

```

#### 4、使用Canvas.createImage()函数创建一个image对象,然后给image对象(src)赋值,在img.onload回调中继续下一步

```javascript
let img = canvas.createImage()

img.src = '临时路径'
img.onload = e => {
	// to do something
}
img.onerror = e => {
	console.log(e)
}
```

#### 5、获取刚刚拍的照片的尺寸(img.width/img.height),然后根据取景框相对于camera组件的位置和大小计算出图片对应部分的截取的定位和尺寸.比如我的取景框的position是top:36.5%,就是c_y = img.height*0.365

```javascript
img.onload = e => {
	this.setData({
		width_t: img.width,
		height_t: img.height
	})
	let c_x = img.width * 0.05
	let c_w = img.width * 0.89
	let c_y = img.height * 0.365
	let c_h = img.height * 0.12

	// 截取图片指定部分并绘制到canvas
	ctx.drawImage(img, c_x, c_y, c_w, c_h, 0, 0, 300, 300 * (c_h / c_w)) // width固定300，按比例计算出height
}
```

#### 6、前面步骤都完成了基本没有大问题了,接下来就是绘制canvas然后保存为图片,存到本地

```javascript

  init(ctx, canvas) {

    let img = canvas.createImage()
    img.src = this.data.iPath
    img.onload = (e) => {

      this.setData({
        width_t: img.width,
        height_t: img.height
      })
      let c_x = img.width * 0.05
      let c_w = img.width * 0.89
      let c_y = img.height * 0.365
      let c_h = img.height * 0.12
     
      console.log(c_x, c_y, c_w, c_h)
      //截取图片指定部分并绘制到canvas
      ctx.drawImage(img, c_x, c_y, c_w, c_h, 0, 0, 300, 300 * (c_h / c_w))//width固定为300,按比例计算出height
      //将canvas内容保存为图片
      wx.canvasToTempFilePath({
        canvas: canvas,
        width: 300,
        height: 300 * (c_h / c_w),
        fileType: 'png',
        success: (res) => {
          wx.saveImageToPhotosAlbum({ //将图片保存到本地相册
            filePath: res.tempFilePath,
          })
          const imgPath = String(res.tempFilePath)
          //上传到接口
          this.uploadimg(imgPath)
        },
        fail: (res) => {
          console.log(res)
        }
      })

    }
    img.onerror = (e) => {
      console.error('err:', e)
    }
  }
```




