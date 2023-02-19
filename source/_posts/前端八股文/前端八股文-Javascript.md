---
title: 前端八股文-Javascript
date: 2023-02-19 17:53:10
tags: 
    - 面试
categories: 
    - 前端
---

### 谈谈对原型原型链的理解？

**构造函数：**与普通函数本质上没什么区别，只是使用了new 关键字，一般首字母大写用以区分普通函数
```js
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.species = '人类'
    this.say = function() {
        console.log('Hello')
    }
}
let per = new Person('张三'， 15)
```

**原型对象：**每个函数类型的数据都有一个叫做prototype的属性，这个属性指向一个对象，这个对象就是原型对象

![原型对象](https://img-blog.csdnimg.cn/57b4ee4d42b744e2b65190e50f5320dc.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81NjUwNTg0NQ==,size_16,color_FFFFFF,t_70#pic_center)

对于原型对象来说，他有个constructor属性，指向它的构造函数
![constructor](https://img-blog.csdnimg.cn/9a73b10ce4dc4f21bf809b82239b0e59.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81NjUwNTg0NQ==,size_16,color_FFFFFF,t_70#pic_center)

原型对象可以用来存放实例对象的公有属性和公有方法
如上方的species属性与say方法，放在构造函数里，那么每创建一个实例，就会重复创建一次相同的属性和方法，浪费。如果把这些公有属性和公有方法放在原型对象里共享，就会好很多。
```js
function Person(name, age) {
    this.name = name;
    this.age = age;
}
Person.prototype.species = "人类";
Person.prototype.say = function() {
    console.log('hello')
}

let per1 = new Person('zhangsan', 15)
let per2 = new Person('lisi', 20)

cosnole.log(per1.species) // 人类
cosnole.log(per2.species) // 人类

per1.say()
per2.say()
```

**原型链：**

1. 显示原型：利用prototype属性查找原型，只是这个函数类型数据的属性
2. 隐式原型：利用__proto__属性查找原型，这个属性指向当前对象的构造函数的原型对象，这个属性是对象类型数据的属性
    __proto__、constructor、prototype三者的关系如图
    ![关系](https://img-blog.csdnimg.cn/e5bdab96716f42d9990a54f4e398dbe2.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81NjUwNTg0NQ==,size_16,color_FFFFFF,t_70#pic_center)

3. 原型链：如果某个对象查找属性，自己和原型对象上都没有，就继续往原型对象的原型对象上去找，直到找到需要的内容或者是null才会结束，这样顺着__proto__属性，一步步向上查找，所形成的一种链式结构，就是原型链
![原型链图解](https://img-blog.csdnimg.cn/1ccbdee4f468444dae832fb574ec733d.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81NjUwNTg0NQ==,size_16,color_FFFFFF,t_70#pic_center)

[！！原作者博客](https://blog.csdn.net/weixin_56505845/article/details/119683904)相当清楚

### Js如何实现继承？
类是拥有共通属性和行为的实体的抽象，对象是一个具体的实例

**继承：**继承是建立在面向对象基础上的一种代码复用方式，子类通过继承复用父类代码
JS继承的最佳实践是“寄生组合式继承”，它用到了原型继承和借用构造函数继承

实现继承的方法：
- 原型继承
    - 实现：子类的prototype = 父类的实例
    - 特点：可以继承父类的私有属性和原型属性
    - 缺点：1、无法向父类的构造函数传参；2、继承的属性都是原型属性，不能是私有属性
- 借用构造函数
    - 实现： 在子类构造函数中使用call/apply调用父类构造函数，将父类构造函数指向子类实例
    - 特点：在子类中可以给父类传参；可以继承父类的私有属性
    - 缺点：只能继承父类的私有属性，不能继承父类的原型属性
- 组合继承
    - 实现：同时使用原型继承与借用构造函数继承
    - 特点：可以给父类传参，能同时继承父类的私有属性与原型属性
    - 缺点：对于父类的私有属性，子类继承时同时存在于私有属性和原型属性中，造成冗余
- 寄生组合式继承
    - 实现：将组合继承中的原型继承去掉，通过另一种方法让子类只继承父类的原型。
    - 特点：可以向父类传参，能继承父类的私有属性与原型属性，继承后没有荣誉

### Js有哪些数据类型？
js高级程序设计：五种简单类型：undefined、null、number、string、boolean，复杂类型：object
实际上，实际上`typeof null`返回值是null，所以，把null归到object去
ES6中又引入了symbol类型
所以，数据类型有以下几种：
- number
- string
- boolean
- object
- function
- undefined
- symbol

undefined只有一个只undefined

数字类型两个特殊值：NaN（非数字）和Infinity（无穷大）

object又可以分为：object、array、date、RegExp

symbol的值是唯一的，用来解决命名冲突；不能与其他值进行运算，不能用for...in遍历

存储位置：
- 基本数据类型：栈内存
- 引用数据类型：指针存在栈中，值存在堆中

堆： 动态分配内存，大小不定，不会自动释放
栈：自动分配内存空间，会自动释放

### Js有哪些判断类型的方法？
**1. typeof**
用来查看字面量或者变量的数据类型，不能具体判断object的类型
```js
typeof 1						// 'number'
typeof '1'					// 'string'
typeof false				// 'boolean'
typeof {}						// 'object'
typeof []						// 'object'
typeof new Date()		// 'object'
typeof (() => {})		// 'function'
typeof undefined		// 'undefined'
typeof Symbol(1)		// 'symbol'
```
**2. instanceof**

判断一个对象的构造函数是否等于给定的值

```js
({}) instanceof Object // true
[] instanceof Array // true
new Date() instanceof Date // true
/123/g instanceof RegExp // true
```
**3. constructor**

**null与undefined没有constructor属性**

```js
console.log(false.constructor === Boolean);// true

console.log((1).constructor === Number);// true

console.log(''.constructor === String);// true

console.log([].constructor === Array);// true

console.log(({}).constructor === Object);// true

console.log((function test() {}).constructor === Function);// true

console.log(Symbol('1').constructor === Symbol);// true
```

**4. Object.prototype.toString**
Object.prototype.toString.call可以用来区分数组、null等引用类型。
```js
function Test(){};
const t = new Test();

Object.prototype.toString.call(1);  '[object Number]'

Object.prototype.toString.call(NaN); '[object Number]'

Object.prototype.toString.call('1'); '[object String]'

Object.prototype.toString.call(true); '[object Boolean]'

Object.prototype.toString.call(undefined); '[object Undefined]'

Object.prototype.toString.call(null); '[object Null]'

Object.prototype.toString.call(Symbol());'[object Symbol]'

Object.prototype.toString.call(Test);  '[object Function]'

Object.prototype.toString.call([1,2,3]); '[object Array]'

Object.prototype.toString.call({});'[object Object]'

Object.prototype.toString.call(t);'[object Object]'

```




### 如何判断一个变量是否为数组？

```js
let arr = [1,2,3]

// 1. ES6 isArray
Array.isArray(arr) // true

// 2. constructor
arr.constructor === Array // true

// 3. instanceof

arr instanceof Array // true

```

### null和undefined的区别？

- null表示引用类型的对象为空，undefined表示未定义
- 类型不同：
    ```js
    console.log(typeof undefined) // undefined
    console.log(typeof null) // object
    ```

### call、apply、bind的区别？
相同点：都可以用来改变this的指向
不同点：
    1. call、apply调用时立即执行，bind调用返回新的函数
    2. 当需要传递参数时，call直接写多个参数，apply将多个参数写成数组，bind在绑定时候需要固定参数时，也是直接写多个参数。

### 防抖和节流的概念？如何实现？

防抖就是防止抖动，避免事件重复触发
节流就是减少流量，将频繁触发的事件减少，并每隔一段时间执行，即，控制事件触发的频率

防抖：某个函数在某段时间内无论触发多少次，都只执行最后一次，如：搜索 
实现原理：函数第一次执行，设定一个定时器，在定时器时间内如果函数再次执行，就清除上一个定时器，重新设定，一直到定时器时间到，才会再次触发
```js
function debounce(fn, delay = 200) {
    let timer = 0

    return function () {
        if (timer) clearTimeout(timer)

        timer = setTimeout(() => {
            fn.apply(this, arguments) // 透传 this 和参数
        }, delay)
    }
}
```
![防抖](https://img-blog.csdnimg.cn/67195cb158274e5f876e358657119449.png)

节流：按时间节奏来，达到某个结果是执行。如：scroll或者drag
    某个操作，希望上一次的完成后再进行下一次，或者希望隔一段时间触发一次

实现原理：函数第一次
```js
function throttle(fn, delay = 100) {
    let timer = 0

    return function () {
        if (timer) return

        timer = setTimeout(() => {
            fn.apply(this, arguments)
            timer = 0
        }, delay)
    }
}
```
![防抖](https://img-blog.csdnimg.cn/14fcee30f3d74ef4841739a448e5f3ca.png)


### 深拷贝与浅拷贝？如何实现？

### var、let、const的区别？

### ES next新特性有哪些？

### 箭头函数与普通函数的区别？

### 使用new创建对象的过程是什么样的？

### this的指向问题？

### 手写bind方法？

### 闭包？应用场景？缺点？如何避免？

### Js事件循环？

### 对于promise的理解？

### 手写promise

### 实现promise.all方法

### CommonJs与ESM的区别？

### 柯里化是什么？有什么用？如何实现？

### 关于JS垃圾回收？

### 实现一个发布订阅？

### 实现数组拍平？

### 实现数组去重？
