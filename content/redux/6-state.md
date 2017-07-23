## connect 的用法

前言：首先一点明确确定：的 react 组件和 redux store 之间是没有任何关系的。这一节，我们就把他们二者 connect 起来。

连接二者，需要一个专门的库，叫做 react-redux，这个是 React 官方的 Redux 对 React 的绑定。


1.首先安装包
```js
npm i --save react-redux
```

2.具体的使用的主要涉及两个接口 Provider 和 connect ，然后在我们平时导出组件的地方换成
```js
export default connect(mapStateToProps)(PostBody=》当前组件的名字);

```

3.详细解释
* connect 连接 store 和组件
* mapStateToProps：把 store 中的数据（一部分）映射为当前组件的 props
map 的意思是“映射”
* State 指的是 store 状态树（ State Tree ），也就是 store 的实际数据
* Porps 就是属性
* Store 中数据很多，当前组件需要的只是一部分，那么选取工作是在 mapStateToProps 中完成的

```js
const mapStateToProps = (state) => ({
  comments: state
});
  comments:自己的写的变量,也可以自己命名
  state,是index 两个或者多个组件合并的在一起的
```

4.connect 完毕之后，PostBody 之中就多了一个属性：this.props.comments

5.只有 connect 不能工作（因为找不着 store），因为 connect 的生效范围是由 <Provider> 组件决定的( Provider 也是一个组件，只有被 Provider 包括起来的组件中才能找得着 store，也就是才能使用 connect)，所以代码中还需要添加

```js
在App js当中写入
<Provider store={store}>
  <div>
    <div className="top  clearfix">
      <PostBody />
    </div>
    <div className="bottom clearfix">
      <CommentBox />
    </div>
  </div>
</Provider>
```


最终修改之后的commments.js 代码   likes的代码  likes.js

```js
let comments=
[
  {
    content:"第一条",
    postId:"1"
  },
  {
    content:"666",
    postId:"1"
  },
  {
    content:"第二条",
    postId:"2"
  }
]
export default function commentReducer(state=comments,action){
  switch(action.type){
    case "ADD_COMMENT":
      return[...state,{content:action.tianjia,postId:action.Id}]
      default:return state
  }

}
```
-------------------------------------------------------

```js
action.Id,action.tianjia Id,tianjia是自己定义的名字
跳转CommentBox

  handleSubmit=(e)=>{
    e.preventDefault()
    // console.log(this.value.value)
    let newComment=this.value.value

    store.dispatch({type:"ADD_COMMENT",tianjia:newComment,Id:this.props.postId})
    console.log(store.getState())
    console.log(this.props.comments)
    // this.value.value=""
    this.word.reset()
  }
  render() {
    let { postId, comments } = this.props
    let myComments= comments.filter(function(item){
        return postId===item.postId
    }
   )
```

##### -store.dispach  是改变state ,相当与es6 中的this.setState({})





点赞 likes.js

```js
let likesPost=[
  {
    postId:"1",
    likes:100,
    title:"Git 技巧"
  },
  {
    postId:"2",
    likes:200,
    title:"学习 Redux"
  }
]



export default function likeReducer(state=likesPost,action){
  switch(action.type){
    case "INCREMENT_LIKE":
    let stateCopy=state.slice()
    // console.log(stateCopy)
    stateCopy.map(item=>{
      if(item.postId===action.Id){
       item.likes++
       return item
      }
         return item
    })
      return  stateCopy
      default:return state
  }
}

```
