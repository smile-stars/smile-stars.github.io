---
title: React中的hooks
date: 2024-02-19 09:40:54
tags:
	- React
main_color: '#a5b6e7'
categories:
	- React
	- 前端
---

## 背景

React-Hooks 是 React 团队在组件开发实践中，逐渐认知到的一个改进点，这背后其实涉及对**类组件**和**函数组件**两种组件形式的思考和侧重

### 类组件

基于 ES6 class 写法，继承 React.Component 得到的组件

```javascript
class Test extends React.Component {
  constructor(props) {
    super(props)
    this.state = { count: 0 } // 数据初始化
    this.change = this.change.bind(this)
  }

  componentDidMount() {
    console.log('mount');
  }

  change(){
    this.setState({count: this.state.count+1})
  }

  render() {
    return <div>
      {this.state.count}
      <button onClick={this.change}>click</button>
    </div>
  }
}
```

可以看到，类组件中内置了很多现成的东西，比如生命周期，我们按照提供的规则去写就能够得到一个可以使用的组件

但React.Component提供的东西太过繁杂，往往难以理解，并且书写的代码逻辑是分散在各个地方，不利于拆分和复用。并且组件常常在 componentDidMount 和 componentDidUpdate 中获取数据，但是，同一个 componentDidMount 中可能也包含很多其它的逻辑，如设置事件监听，而之后需在 componentWillUnmount 中清除。

相互关联且需要对照修改的代码被进行了拆分，而完全不相关的代码却在同一个方法中组合在一起。如此很容易产生 bug，并且导致逻辑不一致。

### 函数组件

就是以函数形态存在的组件，因为一开始并没有 hook，所以函数组件无法定义和维护state，被称为无状态组件

```javascript
function Test(props) {
  const { value } = props
  return <div className="wrapper">
    <span>get some value: {value}</span>
  </div>
}
```

在 hook 出现之前，类组件要明显强于函数组件，函数组件最大的问题是无法维护内部状态

react hooks 的出现，可以让我们在不编写 class 的情况下使用 state 以及其他的 React 特性，补齐函数相对于类组件而言缺失的功能。

没有太多书写的限制，不强制按照生命周期划分逻辑，不需要理解 this，将复杂组件中相互关联的部分拆分成更小的函数达到复用的目的。

### 关于Vue

类组件和函数组件之间，是面向对象和函数式编程这两套不同的设计思想之间的差异，react 16.8 新增 hook 大力推进 函数组件的使用，vue3 新增 composition API 取代 options API 的写法，options API 实际上还是面向对象的思路，composition API 也叫 组合API

- options API 对比 react 类组件：

1、组件数据：vue data 类似于 this.state，数据必须在这里统一初始化

2、功能方法：vue 则限制在 methods里，react 将所有方法分散在 class 里

3、生命周期：vue 和 react 都是通过特定的方法名调用

- vue options API 与 react 类组件遇到的问题很相似：

1、逻辑不好拆分达到复用，和组件强关联

2、不相关的代码组合在一起，相关的代码反而聚合在一起

3、需要注意 this指向

- 为了解决部分问题，vue 和 react 都有一些解决方法：

vue：引入 mixin extends 等但毫无疑问增加了使用和维护成本还带来了数据流向不清晰的问题

react：引入 providers，consumers，高阶组件，render props 等其他抽象层组成的组件最终形成了“嵌套地狱”，同时也存在数据流向的问题

但这说明了一个更深层次的问题：Vue 和 React 都需要为共享状态逻辑提供更好的原生途径。

结果是：

1、vue3 引入 Composition API 与 `<script setup>`

2、react16.8 引入 hook

关于 Composition API：实质就是抛弃了 options 的写法，不再是一个对象，而是将一些逻辑组合在一起，其实就是函数组件

关于 `<script setup>`：vue3 兼容 options API 的写法，并提供了 setup 属性，可以把组合在一起的逻辑写在这里，但如果把 setup 作为 script 标签的属性就可以完全抛弃 options API

从类组件和 options API 从一开始引入到出现种种问题，再到逐步引入了一些新的更为复杂的概念，再到官方推旧出新引入新的设计中可以看到，在组件设计上，尤其是业务组件逐渐复杂的情况下，函数式编程要完胜与面向对象的写法。

## hooks一览

hook 大致分为几种：

1、组件状态处理相关： useState、useReducer、useContext

2、处理副作用：useEffect、useLayoutEffect

3、性能优化相关：useMemo、useCallback

4、DOM 相关：useRef

5、redux 相关：useSelector、useDispatch、useStore

6、用户自定义 hook 或者是 某些库自带的 hook等

### useState

在函数组件保存数据的主要方法，等同于类组件的 this.state 与 this.setState

```javascript
function Test () {
	const [count, setCount] = React.useState(0)
	const change = () => setCount(count++)
	return (
		<div>
			当前count: {count}
			<button onClick="{change}">点击+1</button>
		</div>
	)
}
```

useState接受初始值，返回一个state，以及更新state的函数

```javascript
const [count, setCount] = React.useState(() => {
	let data = 0
	// data = getData() // 可以进行一些计算
	return data
})
```

初始值可以是一个函数

**注意：useState返回的是一个数组

> ?? 为什么是数组，不是对象
> 返回对象需要考虑对象属性名的问题
> const { state, setState } = React.useState({})
> const { state: count, setState: setCount } = React.useState(0)
> 如果使用了多次 setState，就要进行重命名，是非常麻烦的！！

### useEffect

类组件中通常在生命周期中执行副作用，useEffect的作用是补充函数组件无法正确执行副作用的问题
> 你之前可能已经在 React 组件中执行过数据获取、订阅或者手动修改过 DOM。我们统一把这些操作称为“副作用”，或者简称为“作用”。

获取数据的例子：

```javascript
function Test() {
  const [count, setCount] = React.useState(0)
  const [text, setText] = React.useState('')
  const change = () => setCount(count + 1)
  fetch("http://127.0.0.1:5504/react-test/index.html").then(async res => {
    let txt = await res.text()
    setText(txt)
  })
  return <div>
    {count}
    <button onClick={change}>click</button>
    {text}
  </div>
}
```
接口获取文件内容并setText ，并在页面渲染出来，看起来没什么问题，但是当点击按钮的时候请求了两次 html，因为每次数据由变化，都会重新执行 Test

此时我们需要 useEffect

```javascript
function Test() {
  const [count, setCount] = React.useState(0)
  const [text, setText] = React.useState('')
  const change = () => setCount(count + 1)
  React.useEffect(() => {
    fetch("http://127.0.0.1:5504/react-test/index.html").then(async res => {
      let txt = await res.text()
      setText(txt)
    })
  }, [])
  return <div>
    {count}
    <button onClick={change}>click</button>
    {text}
  </div>
}
```

useEffect接受两个参数：

参数一：被监听的参数发生变化时执行的回调函数
参数二：被监听的参数

参数二为空，表示不依赖任何数据，只在初次渲染后触发

当监听参数发生变化时就会执行回调，这里空数组只会在初次渲染时执行，等同于 componentDIdMount

