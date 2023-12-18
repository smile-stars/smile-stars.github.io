---
title: package.json中依赖版本说明
date: 2023-12-18 11:33:01
tags:
categories:
	- 前端
---
## package.json文件示例
```json
{
  "name": "chrome-extension",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build",
    "lint": "vue-cli-service lint",
    "build-watch": "vue-cli-service  --env.NODE_ENV=development build-watch --mode development"
  },
  "dependencies": {
    "axios": "^1.6.2",
    "core-js": "^3.8.3",
    "element-ui": "^2.15.14",
    "jquery": "^3.7.1",
    "js-md5": "^0.8.3",
    "qs": "^6.7.0",
    "vue": "^2.6.14"
  },
  "devDependencies": {
    "@babel/core": "^7.12.16",
    "@babel/eslint-parser": "^7.12.16",
    "@vue/cli-plugin-babel": "~5.0.0",
    "@vue/cli-plugin-eslint": "~5.0.0",
    "@vue/cli-service": "~5.0.0",
    "eslint": "^7.32.0",
    "eslint-plugin-vue": "^8.0.3",
    "vue-cli-plugin-chrome-extension-cli": "~1.1.4",
    "vue-template-compiler": "^2.6.14"
  },
  "eslintConfig": {
    "root": true,
    "env": {
      "node": true,
      "webextensions": true
    },
    "extends": [
      "plugin:vue/essential",
      "eslint:recommended"
    ],
    "parserOptions": {
      "parser": "@babel/eslint-parser"
    },
    "rules": {}
  },
  "browserslist": [
    "> 1%",
    "last 2 versions",
    "not dead"
  ],
  "_id": "chrome-extension@0.1.0",
  "readme": "ERROR: No README data found!"
}
```
## package.json各字段说明

1. `name`名称
2. `version`版本
3. `scripts`执行脚本
4. `dependencies`生产环境依赖
5. `devDependencies`开发环境依赖
6. `eslintConfig` eslint配置
7. `browserslist`浏览器支持情况

## 依赖版本符号说明

1. `^`
`"@babel/core": "^7.12.16"`表示只更新到次版本号，只会从7.12.16更新到7.x.x，不会更新到8.x.x

2. `~`
`"@vue/cli-plugin-babel": "~5.0.0",`表示只更新到补丁版本，只会由5.0.0更新到5.0.x，不会更新到5.1以及6.x

3. 无符号
`"qs": "6.7.0"`表示依赖版本不会更新


