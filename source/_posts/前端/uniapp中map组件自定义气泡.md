---
title: uniapp中map组件自定义气泡
date: 2023-10-18 14:40:01
tags:
	- uni-app
categories: 
	- 前端
---

## 需求描述

小程序中需要对地图打点，同时对打点处气泡自定义样式（文案+图标）

在小程序中 使用uni-app中的map组件加载地图，并对特定位置进行标记（markers）

`markers.callout = {}`可以对标记的气泡进行设置，但是仅支持边框，字号，颜色，背景等基础设置

## 代码演示

### HTML部分
```HTML
<template>
    <view class="map-wrap">
        <map class="map" :markers="markers" :latitude="latitude"
            :longitude="longitude" :scale="16" @markertap="markerTap">
            <cover-view slot="callout">
                <block v-for="(item, index) in customCalloutMarkerIds" :key="index">
                    <cover-view class="customCallout" :marker-id="item">
                        <cover-view class="txt">{{markers[index].locationName}}</cover-view>
                        <cover-image :src="markersImgs[index]" class="content-image"></cover-image>
                    </cover-view>
                </block>
            </cover-view>
        </map>
        <video :src="curVideo" v-if="curVideo"></video>
    </view>
</template>
```

### JS部分

```javascript
<script>
    export default {
        data() {
            return {
                latitude: 34.788195,
                longitude: 113.685064,
                videos:[
                    "https://img.cdn.aliyun.dcloud.net.cn/guide/uniapp/%E7%AC%AC1%E8%AE%B2%EF%BC%88uni-app%E4%BA%A7%E5%93%81%E4%BB%8B%E7%BB%8D%EF%BC%89-%20DCloud%E5%AE%98%E6%96%B9%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B@20200317.mp4",
                    "https://img.cdn.aliyun.dcloud.net.cn/guide/uniapp/%E7%AC%AC1%E8%AE%B2%EF%BC%88uni-app%E4%BA%A7%E5%93%81%E4%BB%8B%E7%BB%8D%EF%BC%89-%20DCloud%E5%AE%98%E6%96%B9%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B@20200317.mp4",
                ],
                markersImgs: [
                    'https://img1.baidu.com/it/u=426464644,1372554843&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=570',
                    "https://img1.baidu.com/it/u=3269176678,389813562&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500",
                ],
                curVideo:"", //当前点击视频
                customCalloutMarkerIds: [1, 2],// 地图markers ID列表
                markers: [{
                    id: 1,
                    latitude: 34.788195,
                    longitude: 113.685064,
                    iconPath: 'https://h5.dhcc.wang/images/huatuitui/group_ic_team.png',
                    width: 32 * 1.5,
                    height: 32 * 1.5,
                    locationName: '动物园',
                    customCallout: {
                        anchorY: -4,
                        anchorX: 0,
                        display: 'ALWAYS', // BYCLICK 点击显示气泡  ALWAYS常显示
                    }
                }, {
                    id: 2,
                    latitude: 34.787256,
                    longitude: 113.673733,
                    iconPath: 'https://h5.dhcc.wang/images/huatuitui/group_ic_team.png',
                    width: 32,
                    height: 32,
                    locationName: '河南省博物院',
                    customCallout: { // 自定义气泡
                        anchorY: -4,
                        anchorX: 0,
                        display: 'ALWAYS', // ALWAYS 总是显示
                    }
                }], 
            }
        },
        methods: {
            markerTap(e) { // 点击标记点时，播放对应的视频
                let markers = this.markers
                markers.find((item, index)=> {
                    if (item.id == e.markerId) {
                        this.curVideo = this.videos[index];
                        item.customCallout.display = 'ALWAYS' // 点击marker 显示地点名
                        item.width = 32 * 1.5; 
                        item.height = 32 * 1.5;  
                    } else {
                        item.customCallout.display = 'NONE';
                        item.width = 32;
                        item.height = 32;
                    }
                })
            }
        }
    }
</script>
```

### CSS 部分

```css
<style lang="less" scoped>
    video{
        position: fixed;
        right:10%;
        bottom:20rpx;
        width: 80%;
        height:200rpx;
    }
    .map-wrap{
        width: 100%;
        height: 100%;
        position: absolute;
        .map{
            width: 100%;
            height:100%;
        }
    }
    .customCallout {
        background-color: #fff;
        background: #FFFFFF;
        box-shadow: 0px 8rpx 32rpx 0px rgba(189, 191, 193, 0.4);
        border-radius: 10rpx;
        padding: 6rpx 24rpx;
        display: flex;
        justify-content: center;
        align-items: center;
        box-sizing: border-box;
        .content-image {
            width: 60rpx;
            height: 60rpx;
            margin-left: 10rpx;
        }
        .txt{
            font-size: 32rpx;
        }
    }
</style>
```

### 实际效果

![实际效果](https://img-blog.csdnimg.cn/a71b4abf25d643d9b9f9d9d65daa5e7b.png#pic_center)




