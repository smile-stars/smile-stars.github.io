---
title: VSCode
date: 2023-03-08 09:48:31
tags:
    - VSCode
categories:
    -  前端
    - HTML
---

## 介绍

Visual Studio Code 是一款非常轻量的前端代码编写工具，也是目前比较主流的。其中还包含了丰富的插件市场、非常好看的界面风格、可在软件内直接使用命令行工具等。

> **建议：** 在学习前端之前可以先把软件下载好，方便实践操作。

***
## 安装

官网地址：https://code.visualstudio.com

![vscode](https://note.noxussj.top/assets/image1.d2db935e.png)
![vscode](https://note.noxussj.top/assets/image2.d0779fa4.png)

***

## 汉化

我们下载完后是英文版的，所以要去 VS Code 的插件市场中去下载中文版插件 `Chinese`

![vscode](https://note.noxussj.top/assets/image3.bbd4aee0.png)

安装插件后，重新启动 VS Code

![vscode](https://note.noxussj.top/assets/image4.90f718d3.png)

***

## 开发习惯配置

以下是我的个人习惯，小伙伴们可以自行看是否需要

设置手动代码提示快捷键

文件 -> 首选项 -> 键盘快捷键方式

或者 Windows 快捷键：`CTRL + K + S`

![vscode](https://note.noxussj.top/assets/image5.8610f379.png)

***

## 扩展插件

VS Code 强大的插件市场，主要介绍几款常用的插件。

> **提示：** 如果你目前用不上这些插件，可以先不用安装。

### One Dark Pro

好看的代码主题

![vscode](https://note.noxussj.top/assets/image6.21b6d2e9.png)

### GitLens — Git supercharged

Git 记录查看工具，方便随时随刻查看某个人某时间点改了某一行代码。方便查看单个文件的修改记录。目前小伙伴们可能用不上，需要先掌握 Git 技术后才能用。

![vscode](https://note.noxussj.top/assets/image7.a40696c6.png)

### Path Autocomplete

URL 路径补充插件，当你需要查找某个 src 路径的时候，它会给你代码提示。例如写 img 标签的 src 路径时候能用上。

![vscode](https://note.noxussj.top/assets/image8.4c264abf.png)

### Vuter

用于高亮 `.vue` 文件的代码，主要适用于 Vue2.0。目前如果用不上可以先不安装。

![vscode](https://note.noxussj.top/assets/image9.e8f95935.png)

### Prettier - Code formatter

用于格式化大部分语言代码，还可以搭配配置文件，自定义格式化风格。

在项目根目录下新建 `.prettierrc` 文件。

```json
{
    "printWidth": 170,
    "tabWidth": 4,
    "semi": false,
    "singleQuote": true,
    "trailingComma": "none"
}

```
![vscode](https://note.noxussj.top/assets/image10.68823e31.png)

### Live Server

可以直接把你的 `.html` 文件部署到服务端。

![vscode](https://note.noxussj.top/assets/image11.85c3d931.png)

## 快捷键大全

列举了比较常用的快捷键方式

| 功能名称 | 快捷键 |  
| :- | :- | 
| 当前文件搜索 | Ctrl + F |
| 全局搜索 | Ctrl + Shift + F |
| 全选 | Ctrl + A |
| 将选中文本转换为大写 | Ctrl + U（需要设置快捷键） |
| 将选中文本转换为小写 | Ctrl + P（需要设置快捷键） |
| 折叠代码 | Ctrl + K + 0~9（代表多少级） |
| 展开折叠代码 | Ctrl + K + J |
| 跳入选中函数方法体 | F12 |
| 复制 | Ctrl + C |
| 粘贴 | Ctrl + V |
| 打开终端 | Ctrl + ~ |
| 删除当前行 | Ctrl + X |
| 撤销更改 | Ctrl + Z |
| 代码换行 | Alt + Z |
| 注释/取消注释 | Ctrl + / |
| 选中多列 | Shift + Alt + 鼠标移动 |
| 连续选中关键词 | Ctrl + D |
| 复制行 | Shift + Alt + ↑ 或者 ↓ |
| 移动行 | Alt + ↑ 或者 ↓ |
| 重命名 | F2 |
| 切换打开文件 | Ctrl + Tab |
| 切换应用 | Alt + Tab |
| 创建HTML5页面结构 | 输入 html5 |
| 跳转到上一个修改处 | Alt + ← |
| 跳转到下一个修改处 | Alt + → |
