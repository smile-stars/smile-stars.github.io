---
title: Picgo + Gitee搭建免费图床
date: 2023-10-21 10:36:15
main_color: "#c0e0e0"
tags:
---

## 前期准备

### 1、Gitee准备

#### 新建仓库

创建一个仓库用来存储上传的图片，选择开源

#### 创建私人令牌-token

> 切记：令牌只显示一次，生成令牌后保存一份，后续要用到，否则就要重新生成

![创建私人令牌](https://cdn.nlark.com/yuque/0/2023/png/21654028/1697856269684-842f154f-004a-4975-8cc0-c90240c95fdf.png)

![创建私人令牌](https://cdn.nlark.com/yuque/0/2023/png/21654028/1697856284243-27d9b309-65ec-40a0-a0e9-379e6f6f7be1.png)



### 2、PicGo下载安装

下载地址：[https://github.com/Molunerfinn/PicGo/releases](https://github.com/Molunerfinn/PicGo/releases)

#### 2.1 gitee插件配置

1、打开PicGo，选择插件设置，搜索并安装`gitee-uploader`

![插件配置](https://cdn.nlark.com/yuque/0/2023/png/21654028/1697856502532-df594e97-f89a-456d-bc49-d2bd27f98f06.png)

2、配置`gitee-uploader`

![配置](https://cdn.nlark.com/yuque/0/2023/png/21654028/1697856604066-77c67e5a-916c-44d6-a12e-cef322282693.png)

![配置](https://cdn.nlark.com/yuque/0/2023/png/21654028/1697856630880-4c8295dc-73b0-49b5-a013-088e63eeabec.png)

- 名称：自定义
- repo：仓库地址
	> 假如你的仓库地址为：`https://gitee.com/zhangsan/zhangsan-image.git`
	> 只需要输入：`zhangsan/zhangsan-image`
- branch：master
- token：第一步中生成的令牌

3、图床设置

选择`gitee`，选中配置好的图床名称，将其设置为默认图床

![配置](https://cdn.nlark.com/yuque/0/2023/png/21654028/1697856958501-5ad8c85d-85f6-4951-a4e7-5458ae41f81d.png)

至此，基本完成，可上传图片。

## 常见问题

1、Error: Error in repo name

此错误是gitee-uploader仓库配置有误，请检查配置。

2、"message": "Not Found Project"

配置仓库地址时，可能添加了`.git`后缀，请检查

3、"message": "Branch"

配置的分支有误，如配置了`master`，但是对应仓库未进行初始化，故没有`master`分支


