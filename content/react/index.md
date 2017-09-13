<h2>前端学习笔记</h2>
<p>面试题</p>

#### 小公司面试题最常见一个问题：
* 谈谈你对web前端的理解
WEB前端是由网页设计与制作发展而来的，随着工作的细化，需要有人完成美工图到网页的制作，从而出现了WEB前端开发这个词。WEB前端开发主要是使用HTML、CSS、JavaScript技术，将美工提供的美工图转化为网页。同时，需要顾及SEO以及后台的数据。WEB前端，相当于是一个连接美工、后台以及用户的中间平台。

* sessionStorage 、localStorage 和 cookie 之间的区别
共同点：都是保存在浏览器端，且同源的。区别：cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递。而sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。cookie数据还有路径（path）的概念，可以限制cookie只属于某个路径下。存储大小限制也不同，cookie数据不能超过4k，同时因为每次http请求都会携带cookie，所以cookie只适合保存很小的数据，如会话标识。sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。数据有效期不同，sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持；localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。作用域不同，sessionStorage不在不同的浏览器窗口中共享，即使是同一个页面；localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的。Web Storage 支持事件通知机制，可以将数据更新的通知发送给监听者。Web Storage 的 api 接口使用更方便。



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
在ES6中，一个React组件是用一个class来表示的（具体可以参考官方文档），如下：
```js
// 定义一个TodoList的React组件，通过继承React.Component来实现
class TodoList extends React.Component {
  ...
}
```

* 这几个生命周期相关的函数有：
```js
constructor(props, context)
```

* 构造函数，在创建组件的时候调用一次。
```js
void componentWillMount()
```

* 在组件挂载之前调用一次。如果在这个函数里面调用setState，本次的render函数可以看到更新后的state，并且只渲染一次。
```js
void componentDidMount()
```

* 在组件挂载之后调用一次。这个时候，子主键也都挂载好了，可以在这里使用refs。
```js
void componentWillReceiveProps(nextProps)
```
* props是父组件传递给子组件的。父组件发生render的时候子组件就会调用componentWillReceiveProps（不管props有没有更新，也不管父子组件之间有没有数据交换）。

```js
bool shouldComponentUpdate(nextProps, nextState)
```

* 组件挂载之后，每次调用setState后都会调用shouldComponentUpdate判断是否需要重新渲染组件。默认返回true，需要重新render。在比较复杂的应用里，有一些数据的改变并不影响界面展示，可以在这里做判断，优化渲染效率。
```js
void componentWillUpdate(nextProps, nextState)
```

* shouldComponentUpdate返回true或者调用forceUpdate之后，componentWillUpdate会被调用。
```js
void componentDidUpdate()
```

* 除了首次render之后调用componentDidMount，其它render结束之后都是调用componentDidUpdate。

componentWillMount、componentDidMount和componentWillUpdate、componentDidUpdate可以对应起来。区别在于，前者只有在挂载的时候会被调用；而后者在以后的每次更新渲染之后都会被调用。

```js
ReactElement render()
```
* render是一个React组件所必不可少的核心函数（上面的其它函数都不是必须的）。记住，不要在render里面修改state。
```js
void componentWillUnmount()
```

#### * 更新方式 *
在react中，触发render的有4条路径。

以下假设shouldComponentUpdate都是按照默认返回true的方式。

首次渲染Initial Render
调用this.setState （并不是一次setState会触发一次render，React可能会合并操作，再一次性进行render）
父组件发生更新（一般就是props发生改变，但是就算props没有改变或者父子组件之间没有数据交换也会触发render）
调用this.forceUpdate






#### 9.ForEach 和 Map区别
* 相同点：

都是循环遍历数组中的每一项
forEach和map方法里每次执行匿名函数都支持3个参数，参数分别是item（当前每一项）、index（索引值）、arr（原数组）
匿名函数中的this都是指向window
只能遍历数组
接下来我们看看这两个方法
callback: 为数组中每个元素执行的函数,该函数接收三个参数，

参数一：当前数组中元素；参数二：索引； 参数三：当前数组。

this：可选，执行会掉时候，this的指向。

二、区别

1、forEach()返回值是undefined，不可以链式调用。

2、map()返回一个新数组，原数组不会改变。

3、没有办法终止或者跳出forEach()循环，除非抛出异常，所以想执行一个数组是否满足什么条件，返回布尔值，可以用一般的for循环实现，或者用Array.every()或者Array.some();

4、$.each()方法规定为每个匹配元素规定运行的函数，可以返回 false 可用于及早停止循环。


```js
var ary = [12,23,24,42,1];
var res = ary.forEach(function (item,index,input) {
     input[index] = item*10;
})
console.log(res);//-->undefined;
console.log(ary);//-->会对原来的数组产生改变；
```

map:和forEach非常相似，都是用来遍历数组中的每一项值的，用来遍历数组中的每一项；
区别：map的回调函数中支持return返回值；return的是啥，相当于把数组中的这一项变为啥（并不影响原来的数组，只是相当于把原数组克隆一份，把克隆的这一份的数组中的对应项改变了）；
不管是forEach还是map 都支持第二个参数值，第二个参数的意思是把匿名回调函数中的this进行修改。
```js
var ary = [12,23,24,42,1];
var res = ary.map(function (item,index,input) {
     return item*10;
})
console.log(res);//-->[120,230,240,420,10];
console.log(ary);//-->[12,23,24,42,1]；
```


#### 5.react总结
React单向数据流：

React是单向数据流，数据主要从父节点传递到子节点（通过props）。

如果顶层（父级）的某个props改变了，React会重渲染所有的子节点。

### props
props是property的缩写，可以理解为HTML标签的attribute。

不可以使用this.props直接修改props，因为props是只读的，props是用于整个组件树中传递数据和配置。
在当前组件访问props，使用this.props。+
