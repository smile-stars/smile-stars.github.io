---
title: 初识TypeScript
date: 2023-02-25 22:43:10
tags:
    - TypeScript
categories: 
    - 前端
---

### 安装

全局安装TypeScript
`npm install -g typescript`
验证是否成功
`tsc -V`
输出版本号，安装成功

### 编译
1. 手动编译
    `tsc 文件名.ts`

2. vscode自动编译
    - 先生成配置文件
    `tsc --init`会生成配置文件，在配置文件中可以进行配置
    - vscode->终端->运行任务->显示所有任务->ts:监视tsconfig.json

