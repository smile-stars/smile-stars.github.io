---
title: 前端八股文-Vue
date: 2023-02-19 23:11:44
tags: 
    - 面试
categories: 
    - 前端
    - Vue
---

### Vue双向绑定原理？
采用Object.defineProperty对数据进行劫持，编译时，对于用到data中数据的地方创建一个watcher来监听数据变化，然后结合发布订阅模式，在数据变动时发布消息给订阅者，从而触发响应我的回调更新视图

### Vuex的使用方法？

Vuex的数据流是组件中触发action，action提交mutations，mutations修改states。 组件根据 states或getters来渲染页面。

原理：Vuex首先创建一个数据中心，然后通过发布订阅的模式去通知订阅者进行修改

Vuex是一个状态管理工具，主要是解决不同组件之间的数据共享问题

Vuex包含的API：
- state
- getters
- mutations
- actions
- module
- 辅助函数：mapState,mapGetters,mapMutations,mapActions
- createStore

`state`和`getters`用来保存状态；
`mutations` 和 `actions`用来改变状态；
监听状态用的是Vue中的`computed`属性;
`module`是用来组织整个应用的状态管理代码，使状态划分模块，易于管理；
辅助函数用来在监听状态时简化代码；
`createStore`用来创建状态管理对象。

注意：Vuex只允许存在一个store对象，当有不同的模块时，需要使用module进行管理，如：
```js
import { createStore } from 'Vuex'

const moduleA = {
    state: {
        name: 'a'
    }
}
const moduleB = {
    state: {
        name: 'b'
    }
}

const store = createStore({
    modules: {
        a: moduleA,
        b: moduleB
    }
})

console.log(store.state.a.name) // a
console.log(store.state.b.name) // b
```

### action与mutation的区别？

两者都可以用来更新状态

action提交的是mutation，而不是直接更新状态；可以包含任意的异步操作。如果需要请求接口，可以在action中进行
mutation只是简单的变更状态，属于同步操作，只能执行同步代码

mutation只能执行同步代码，可以直接更新状态。
action同样可以更新状态，只是action是通过提交mutation的方式对state进行更新。`store.commit('xx'，value)`

### 为什么mutation同步，action异步

- mutations里同步的意义在于，每一个mutation执行完毕之后，可得到对应的状态，方便Vuex的devtools工具可以跟踪状态的变化
- 如果在mutations中写入异步，devtools工具就没法知道状态是什么时候更新的，所以才有了actions
- actions用来专门处理异步，里面触发mutations，就可以很清楚的看到mutation是何时被记录下来的，并且可以立即查看对应的状态，这样异步更新也可以看到更新状态的流程；

### 数据持久化存储？
> 原因：Vuex是基于内存的，状态存在于内存里面的，刷新网页之后就没有了，不会持久化存储

**解决方案**：以token为例（用户登录信息）
**实现思路**：只要Vuex中的数据发生变化，九自动往本地同步一份

**实现步骤**
1. 安装`vuex-persistedstate`来支持持久化
2. 在store入口文件中配置
```js
import {createStore} from 'vuex'
const store = createStore({
    modules: {
        moduleA
    },
    state: {},
    getters: {}.
    mutations: {},
    actions: {},
    plugin: [
        createPersistedstate({
            key: 'user', // 存数据的key名，最好语义化，知道是干嘛用的
            paths: ['xxx'], // 要进行数据持久化的模块,与modules中的名字一致
            storage: window.sessionStorage // 数据存储到哪里，默认是localStorage
        })
    ]
})
```


### MVVM与MVC的区别？

MVVM即Model-View-ViewModel的简写。即模型-视图-视图模型。
模型（Model）指的是后端传递的数据。
视图(View)指的是所看到的页面。
视图模型(ViewModel)是mvvm模式的核心，它是连接view和model的桥梁。

MVC是Model-View- Controller的简写。即模型-视图-控制器。
M和V指的意思和MVVM中的M和V意思一样。
C即Controller指的是页面业务逻辑。
使用MVC的目的就是将M和V的代码分离。
MVC是单向通信。也就是View跟Model，必须通过Controller来承上启下

### Vue组件间通信方式？

1. `props`与`$emit`
适用于父子组件之间的数据传递
父组件中通过属性将数据传递给子组件，在子组件中通过props进行接收
- 父传子
```html
<!-- 父组件 -->
<child msg="I'm child"></child>
```
```js
// 子组件
// <div>{{msg}}</div>

export default {
    el: '#app',
    props: {
        msg: {
            type: String,
            default: ''
        }
    }
}
```

- 子传父
在子组件中通过$emit调用父组件的方法，将数据传递给父组件

```js
// 子组件
this.$emit('funcName', value)
```
```js
// 父组件
// <child @funcName="getChildData"></child>

function getChildData(childData) {
    console.log(childData)
}
```
2. `$refs`
父组件能通过$refs直接调用子组件的方法

```js
// 父组件
<child ref="childRef"></child>

// js
this.$refs.childRef.getChildFunc()
```

3. 自定义事件`eventBus`
适用于各种层级关系的组件之间进行通信
`eventBus`是一个典型的发布订阅模式，当状态改变的时候，改变方通过`eventBus`发布状态改变事件，相关订阅者则通过该事件获取最新状态进行更新

```js
// 通过定义一个Vue对象来实现`eventBus`
const eventBus = new Vue()

eventBus.$on('自定义事件名', (接收参数)=>{ // 接收数据一方
    console.log('我是TestB组件，收到了数据', 接收参数);
  })
eventBus.$emit('自定义事件名', 传递参数) // 传递数据一方
eventBus.$off() // 解除绑定

```

4. Vuex

5. `$parent`与`$children`
适用于直接父组件或者子组件，注意：$children是非响应式的

6. `provide`与`inject`
适用于不同层级组件的通信

在上级组件定义provide

在下级所有组件都能接收数据inject

```js

provide: {
    msg: 'hello'
}
// 或
provide() {
    return {
        msg: 'hello'
    }
}

inject: ['msg']
```
### Vue组件中为什么data是一个函数

1. Vue的组件是复用的，为了防止data数据的复用，将data定义为函数
2. vue组件中的data数据都应该是相互隔离，互不影响的，组件每复用一次，data数据就应该被复制一次，之后，当某一处复用的地方组件内data数据被改变时，其他复用地方组件的data数据不受影响，就需要通过data函数返回一个对象作为组件的状态。

3. 当我们将组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一份新的data，拥有自己的作用域，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。

4. 当我们组件的date单纯的写成对象形式，这些实例用的是同一个构造函数，由于JavaScript的特性所导致，所有的组件实例共用了一个data，就会造成一个变了全都会变的结果。


### computed与watch的区别？

1. 应用场景不同
    computed用在根据已有属性或者值计算得到新值的情况
    watch用在监听已有值的变化
2. 执行过程不同
    computed所依赖的值没有发生变化，不会重新进行计算，而是等到访问的时候再判断（有缓存）
    watch所依赖的值发生变化后就会执行watch的会调

### v-for与v-if同时使用有什么问题？

两者同时使用，会在每次渲染时候都要遍历列表并判断是否需要渲染，没有必要

### 前端路由原理。比较一下history与hash两种路由
默认hash模式，路径上会有#

原理：
    1. 可以修改url，但不会引起刷新，从而在不刷新的页面的情况下跳转路由。
    2. 监听url改变，根据url渲染对应组件

hash是通过浏览器提供的location API修改url，通过onhashchange方法监听hash改变

history通过浏览器提供的history.pushState或者history.replacestate修改url，通过popState事件监听url改变

### Vue的虚拟Dom，原理？好处？对比手动操作Dom一定是最优的吗？

vdom是一个用来描述真是DOM的js数据结构，vdom是树状结构，每个节点对应dom的元素，保存了dom元素的标签名，属性，子节点等信息。
node节点的几种类型：TextVNode、ElementVNode、ComponentVNode等



**虚拟DOM的优点**
- 维护视图与状态的关系，在状态改变后，Vue会生成新的虚拟DOM，然后与旧的虚拟DOM进行对比，得到区别，从而进行patch，更新真是DOM，从而保持视图和状态一致

- 避免手工操作DOM，提升项目的可维护性

- 跨平台

**虚拟DOM很多时候都不是最优的操作，但它具有普适性，在效率、可维护性之间达平衡**

减少DOM操作提升性能的本质：主要是虚拟dom使修改元素的操作都脱离了文档流，减少重排和重绘，因此提升了性能。

### Vue的keep-alive使用以及原理

keep-alive是vue的一个内置组件,它将不活动的组件保存在内存中,而非只将其销毁,提供了include(缓存),exclude(不缓存)两个属性,可以有选择的保存组件

### Vue 父子组件生命周期的触发顺序

1. 加载渲染过程
    父beforeCreate-》父created-》父beforeMount-》子beforeCreate-》子created-》子beforeMount-》子mounted-》父mounted

2. 更新过程
    父beforeUpdate-》子beforeUpdate-》子updated-》父updated

3. 销毁过程
    父beforeDistory-》子beforeDistory-》子distoryed-》父distoryed

### Vue.nextTick的实现？


### Vue的diff算法

作用：用来修改DOM的一小段，不会频繁引起DOM树的重绘

diff算法将虚拟DOM的某个节点数据改变后生成新的的node节点与旧节点进行比较，并替换为新的节点，具体过程就是调用Patch方法，比较新旧节点，一边比较一边给真实DOM打补丁进行替换

### Vue中key的作用？

主要是为了高效的更新dom, 其原理是vue在patch过程中通过key更精准判断俩两个虚拟DOM是否是同一个,从而避免频繁更新不同元素,使得整个patch过程更加高效,减少dom操作,提高性能

### Vue2与Vue3的区别？
1. 响应式原理不同。
    - Vue2主要是通过Object.defineProperty对数据进行监听，通过发布订阅模式，将变动的数据通知给订阅者，从而进行视图更新
    - Vue3是通过proxy来实现响应式。通过 reactive() 函数给每⼀个对象都包⼀层 Proxy，通过 Proxy 监听属性的变化，从⽽ 实现对数据的监控。
2. 数据和方法的定义方式
    - Vue2是通过选项式API来定义数据与方法
    - Vue3是通过组合式API来定义数据与方法setup()

### Vue3 新特性

1. 通过proxy实现响应式
2. 组合式API：代码组织更方便了, 逻辑复用更方便了 非常利于维护!!
3. template不再强调只有一个根元素，可以有多个元素
4. ref与reactive函数。Vue3中setup定义的数据默认是非响应式的，可以通过ref与reactive来定义响应式数据
5. toRefs函数：对一个 **响应式对象** 的所有内部属性, 都做响应式处理, 保证展开或者解构出的数据也是响应式的( 一般配合 `reactive` 使用)
    - reactive 的响应式功能是赋值给对象的, 如果给对象解构或者展开, 会让数据丢失响应式的能力
    - 使用 toRefs 可以保证该对象展开的每个属性都是响应式的

    ```html
    <script setup>
        const defaultData = reactive({
            name: '',
            age: 10,
            formData: {
                color: ''
            }
        })

        const {name, age, formData} = toRefs(defaultData) // 解构出的name、age、formData都是响应式数据
    </script>
    ```


### Pinia是什么？好处？

Pinia是一个状态管理工具，实现不同组件间数据共享

相关API
state、getters、action

好处：
- 与Vuex相比，体积小，轻巧
- 更完整的支持TS
- 支持多个Store
- 没有modules配置，每一个独立的仓库都是defineStore生成出来的
