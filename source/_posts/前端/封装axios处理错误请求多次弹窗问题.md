---
title: 封装axios处理错误信息弹窗多次弹出问题
date: 2023-11-06 09:40:12
categories:
	- 前端
---

# 问题描述

前端处理请求时，一般会封装请求方法，对返回内容以及错误信息进行统一管理，但是当同时请求多个信息且发生报错时，平常的方式会对每一个请求接口进行窗口提示，就会同时弹出多个弹窗，用户体验及其不好

![多个弹窗](https://gitee.com/syy1101/image/raw/master/20231106.png)

# 处理方案

> 个人使用的是elementUI，故本文针对elementUI进行处理

**方案：重写message弹窗**

### 第一步，重写message

创建resetMessage.js

```javascript
/**重置message，防止同时多个重复弹出message弹框 */
import { Message } from 'element-ui'
let messageInstance = null
const resetMessage = (options) => {
    if (messageInstance) {
        messageInstance.close()
    }
    messageInstance = Message(options)
};
['error', 'success', 'info', 'warning'].forEach(type => {
    resetMessage[type] = options => {
        if (typeof options === 'string') {
            options = {
                message: options
            }
        }
        options.type = type
        return resetMessage(options)
    }
})
let messageup = null
export default messageup = resetMessage

```

### 第二步：在main.js中引入

> 注意：重写message提示框  一定要放在Vue.use(ElementUI)之后

```javascript
import Message from './assets/js/resetMessage';
Vue.use(ElementUI);
Vue.prototype.$message = Message; // 重写message提示框  一定要放在Vue.use(ElementUI)之后
```

### 使用方法

1. 在vue组件中调用

```javascript
this.$message.error('提示内容'); // 方式一
this.$message({type:success,message:'提示内容'}); // 方式二
```

2. 在js文件中调用

需要先引入resetMessage.js

```javascript
import Message from '@/utils/resetMessage';
 
Message({type: 'error',message: '提示内容'});// 方式一
Message.error('提示内容'); // 方式二
```





