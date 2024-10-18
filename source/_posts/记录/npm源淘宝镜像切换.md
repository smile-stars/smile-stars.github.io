---
title: NPM源淘宝镜像切换
date: 2024-10-18 09:46:14
sticky: 999999
tags:
  - 记录
---

# 🎀NPM

**全局设置**

1. 查看镜像地址

```
npm config get registry
```

2. 设置淘宝镜像

```
// 推荐地址
npm config set registry https://registry.npmmirror.com
 
npm config set registry https://registry.npm.taobao.org
```

3. 还原默认镜像

```
npm config set registry https://registry.npmjs.org
```

**临时使用**

1. 临时使用一次淘宝镜像

```
npm --registry https://registry.npm.taobao.org install XXX（模块名）
```

**CNPM**

1. 全局安装

```
npm install -g cnpm --registry=https://registry.npmmirror.com
```

# 🎨YARN

1. 查看镜像地址

```
yarn config get registry
```

2. 设置淘宝镜像地址

```
// 设置镜像地址为淘宝（地址1，推荐）：
yarn config set registry https://registry.npmmirror.com

// 设置镜像地址为淘宝（地址2）：
yarn config set registry https://registry.npm.taobao.org
```
3. 还原默认镜像地址

```
yarn config set registry https://registry.yarnpkg.com
```

# 🎪PNPM

1. 查看镜像地址

```
pnpm config get registry
```

2. 设置淘宝镜像地址

```
// 设置镜像地址为淘宝（地址1，推荐）：
pnpm config set registry https://registry.npmmirror.com

// 设置镜像地址为淘宝（地址2）：
pnpm config set registry https://registry.npm.taobao.org
```
3. 还原默认镜像地址

```
pnpm config set registry https://registry.npmjs.org
```

# 🍕YARN相关问题

1. yarn create vue创建项目出现“文件名、目录名或卷标语法不正确”的错误

> 出现该错误，有可能是yarn bin的目录和yarn的全局安装模版目录不在同一个硬盘分区下。

**查看npm全局包位置**

```
npm config get prefix
```

**查看npm缓存位置**

```
npm config get cache
```

**查看yarn命令目录**

```
yarn global bin
```

**查看npm全局包位置**

```
npm config get prefix
```