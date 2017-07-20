任务一： 显示几条评论在页面上

### 1.首先在一个组建上创建
```js
this.state = {
  comment1: "hello1",
  comment2: "hello2"，
}
```

### 2.添加个form表单

```js
<div className="comment-box">
  {commentList}
  <form ref={word=>this.word=word} className="comment-form" onSubmit={this.handleSubmit}>
    <input ref={xxx=>this.value=xxx} className="input" type="text"/>
    <button type="submit" className="submit-btn" >提交</button>
  </form>
  <div className="underline"></div>

</div>
```


### 3.发布评论
发布评论的过程：

-点一下 submit 这个按钮，浏览器发成的 event （事件）就是 “表单提交（ form submit ）”
-事件触发之后，我们如何来写对应的”事件处理函数“一般会叫 handleXXX ，意思是”处理XXX事件“
-如何把”事件处理函数“跟事件本身绑定起来呢？纯 html 中用 action 属性来处理。但是有了 React 就不用 action 。用 onSubmit （ on 的意思就是”当发生“ )


```js
  <form onSubmit={this.handleSubmit} />
```

然后在这个时间写上阻止跳转
```js
传参数e    e.preventDefault()
例子如下：
handleSubmit=(e)=>{
  e.preventDefault()
  // console.log(this.value.value)
  let newComment=this.value.value

  store.dispatch({type:"ADD_COMMENT",tianjia:newComment})
  // this.value.value=""
  this.word.reset()
}
```


下一步就需要拿到用户填写的评论内容了，这个我们就不用 refs 了。而改用箭头函数。


```js
<input ref={(value) => { this.textInput = value} }
```
