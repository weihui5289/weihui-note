<h2>前端学习笔记</h2>
<p>面试题</p>

#### 1. react-redux和react-router-redux有什么区别
react-redux:把react的state 集成到redux的store上，让redux来管理react组件的状态
react-router-redux：把react-router url的变化、参数等信息作为状态，交给redux的store管理，一般场景下直接使用react-router即可，因为url的这些状态比较独立，不一定非要交给redux来管理的。

#### 2. state和props区别
state和props主要区别props是不可以改变的的。state通过用户交互进行改变，而props通过父组件来进行改变，state可以通过自身组件改变

#### 3.react结合redux 流程图
React-Redux 将所有组件分成两大类：UI 组件（presentational component）和容器组件（container component）。
>只负责 UI 的呈现，不带有任何业务逻辑
没有状态（即不使用this.state这个变量）
所有数据都由参数（this.props）提供
不使用任何 Redux 的 API

* 容器组件
>负责管理数据和业务逻辑，不负责 UI 的呈现
带有内部状态
使用 Redux 的 API

UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑。



#### 4. <Provider>组件
connect方法生成容器组件以后，需要让容器组件拿到state对象，才能生成 UI 组件的参数。
一种解决方法是将state对象作为参数，传入容器组件。但是，这样做比较麻烦，尤其是容器组件可能在很深的层级，一级级将state传下去就很麻烦。
React-Redux 提供Provider组件，可以让容器组件拿到state。
```js
import { Provider } from 'react-redux'
import { createStore } from 'redux'
import todoApp from './reducers'
import App from './components/App'

let store = createStore(todoApp);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
  ```
  上面代码中，Provider在根组件外面包了一层，这样一来，App的所有子组件就默认都可以拿到state了。

  #### 5. React-Router 路由库

  使用React-Router的项目，与其他项目没有不同之处，也是使用Provider在Router外面包一层，毕竟Provider的唯一功能就是传入store对象。
  ```js
  const Root = ({ store }) => (
  <Provider store={store}>
    <Router>
      <Route path="/" component={App} />
    </Router>
  </Provider>
);
```

#### 5.React 中 keys 的作用是什么？
Keys 是 React 用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识


#### 6.传入 setState 函数的第二个参数的作用是什么？
传入 setState 函数的第二个参数的作用是什么？

#### 7. react与redux 原理工作流程
1.首先用redux管理数据  2.然后用Provider组件向各个组件传递store 实现数据通信
3.通过this.props.dispatch将数据传递到redux
4.然后用action触发reducer函数返回新的state改变接收数据的内容

* 官方解释
Provider组件接受redux的store作为props，然后通过context往下传。

二、connect函数收到Provider传出的store，然后接受三个参数mapStateToProps，mapDispatchToProps和组件，并将state和actionCreator以props传入组件，这时组件就可以调用actionCreator函数来触发reducer函数返回新的state，connect监听到state变化调用setState更新组件并将新的state传入组件。

connect可以写的非常简洁，mapStateToProps，mapDispatchToProps只不过是传入的回调函数，connect函数在必要的时候会调用它们，名字不是固定的，甚至可以不写名字。


#### 8.请描述React组件加载时生命周期执行顺序，组件更新时生命周期执行顺序
* 1.componentWillMount()
仅在render()方法前被调用一次，如果在该方法中调用了setState方法去改变组件的状态值，那么调用render()后，将会直接看到改变过了的状态值，并且不论状态值怎么改变，componentWillMount()都不会再被调用。
* 2.
