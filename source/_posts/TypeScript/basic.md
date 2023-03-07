---
title: TS基础
date: 2023-02-25 23:11:47
tags:
    - TypeScript
categories: 
    - 前端
---


### 原始数据类型
`boolean`、`string`、`number`等
1. 类型声明
可以指定变量，函数返回值等的类型.ts编译器会自动检查是否符合类型声明，不符合报错
`let str:string = 'zhang'`

```js
function test(a: number):number {
    return a + 10
}
```

2. 数字类型，支持10进制，二进制，十六进制等

`let a:number = 10 // 十进制`
`let a:number = 0b1010 // 二进制`
`let a:number = 0o12 // 八进制`

3. undefined与null

`let u:undefined = undefined`
`let u:null = null`
> 还可以作为其他类型的子类型
> 可以把undefined与null赋值给其他类型的变量
如：`let a:number = undefined`

### 引用类型 

数组、对象等

1. 数组
- 方式一：
`let arr:number[] = [1,2,3]`
arr是数组类型，且数组的元素必须是数字

- 方式二：通过泛型去定义一个数组
`let arr:Array<number> = [1,2,3]`
指定变量的类型，后面跟`<>`，括号内指定数组子元素的类型

2. 对象
表示非原始类型：number\string\boolean之外的类型
`let obj:object = {}`

3. any
任何类型
`let a:any = 123`
`a = 'aa'`
`a = {}`

4. void
表示空值,表示没有任何返回值的函数,更多用在函数上

```ts
function func1():void {
    console.log(123)
}
console.log(func1) // undefined
```

`let u:void = undefined`


### 类型推断
如果没有明确制=指定类型，TypeScript会按照类型推论的规则推断出一个类型
- 第一种：有初始值
```ts
let a = 1 // 没有给变量a指定类型，所以会推断出a的类型是number，再给a赋值时，赋值其他类型的值会报错

a = [] // 报错
a = 'aa'
```
- 第二种：没有初始值
```ts
let g; // g没有初始值，则推断g的类型为any，后续可以给g赋值任何类型

g = 123 // 正常
g = [] // 正常
```

### 联合类型
表示取值可以为多种类型中的一种

```ts
let f:boolean | number = true // f可以是boolean与number其中的一种

f = 123 // 正常

f = 'str' // 报错
```

> 当TS不确定一个联合类型的变量到底是哪个类型的时候，我们只能访问此联合类型所有类型里共有的属性或者方法