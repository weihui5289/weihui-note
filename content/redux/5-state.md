### Redux 是数据流管理工具。使用 Redux 的最重要的一句话：

`一切数据都要保存的 Store 之中，组件自己不保留自己的 state 数据`

把所有的数据都存放到 Store 中，然后所有的组件都订阅 Store 的数据。那么数据就有了 Single Source of Truth （唯一可信数据源）。这样的好处就是：

* 第一，各个组件都统一读写同一个数据，组件间通信变得不成问题了
* 第二，就是数据统一存放，代码比较不容易写乱

## 创建 Store ？创建个store.js
```js
let comments = [
    "hello1",
    "hello2"
]
```


但是，store 中的数据，必然要涉及读和写的操作，所以我们要安装 一个包来辅助后续操作：
```js
npm i --save redux
```

到 store.js 中先导入
```js
import { createStore } from 'redux'
```

我们可想象到的就是， store.js 中会做这样的导出

```js
let store = createStore(comments)
export default store
```


### 最终的代码

```js
import {createStore} from "redux"
import rootReducer from "./reducers/index"

let store = createStore(rootReducer)
export default store

```


reducer ，这一项是必须填写的
preloadedState，预加载 State ，这一项是可选的
enhancer，增强器，选填
小贴士：如何快速找到接口文档。答案就是用 google 搜索。会用 google 和科学上网是程序员的基本素质。接口文档上，有中括号的参数是可选的（ optional ）


###reducer
下面是个小例子

```js
function commentReducer(state = [], action) {
  // console.log(state, action);
  switch (action.type) {
    case 'ADD_COMMENT':
      // console.log([...state, action.comment])
      return [...state, action.comment]
    default:
      return state;
  }
}
```


上面的代码我们先不用理解，只需要知道 reducer 的基本格式是：
```js
(oldState, action) => nextState

```


但是我们这里先写一个空的 reducer ：

```js
function commentReducer(state = [], action) {
  return state;
}
```





### 修改 Store 中的数据
前面实现了从 Store 中通过 store.getState() 读数据。下面我们来实现修改数据的操作。这个主要通过 Redux 三大概念的，另外两个：action ， reducer 来配合使用。

基本原理：组件发出 action ，action 触发 reducer ，真正修改 数据，是通过 reducer 来完成。

### 先来看 action
前面的用词是组件发出 action 可见 action 是名词。那么 redux 这里 action 其实就是一个如下的对象：

```js
let action = {
  type: 'ADD_COMMENT',
  comment: "hello3"
}
```


action 对象有两个部分组成：

-第一部分，要有一个 type 属性，值是一个字符串。
-第二部分，payload ，也就是这个 action 携带的数据
-上面的这个形式，让我们联想起了 axios 发 POST 请求（action 的接受方就是 reducer）。

发出一个 action 就是在组件内部

```js
store.dispatch(action)
```

dispatch 就是发出（分发）的意思，可以用它发出 action 。

发出之后，需要有专门对应的 reducer 进行接收。




### Reducer
它的作用就是接受 action ，然后根据 action 修改 store 中的数据。

这样：每次 dispatch action 之后，reducer 都可以去修改 state 值了。

整个 store 中存储的 state 值，我们会把它叫做状态树 ( state tree ) 。状态树的具体值就是 store.getState() 的返回值。整个项目，只有一个状态树。

### 修改数据的时间维度的执行流程
首先，用户点提交按钮

```js
store.dispatch({type, payload})
```
然后，由 store.js 中的 commentReducer 来接收。

```js
function commentReducer(state = [], action) {
  // console.log(state, action);
  switch (action.type) {
    case 'ADD_COMMENT':
      // console.log([...state, action.comment])
      return [...state, action.comment]
    default:
      return state;
  }
}
```

也就是 commentReducer 要开始执行，执行的时候，state 是什么呢？

我们可以看到 commentReducer 中 state 的默认值是 [] ， 也就是说如果 state 我们不给它赋值，后续执行中它的值就是 []

并且这里比较奇怪的是，我们也没又看到 commentReducer 的调用语句，类似

```js
let state = [
...
]
commentReducer(state, action)
```


所以感觉上是是没有给 state 。但是，其实 redux 采用的是函数式编程的思想。

commentReducer 的调用是在

```js
const store = createStore(commentReducer, comments);
```
