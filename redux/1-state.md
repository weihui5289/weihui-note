现在实现表单提交事件，添加handeleSubmit

 ```
 <form ref="commentForm" onSubmit={this.handleSubmit}   className="comment-form">
          <input ref={(value) => { this.textInput = value} } type="text" className="input" />
          <button type="submit" className="submit-btn" >提交</button>
        </form>

```
名词解释：
-submit "提交"
-handle "处理"
-form   "表单"

然后定义 handleSubmit

```js
handleSubmit=()=>{

}

```

由于使用了胖箭头的语法所以不用bind(this)

```js
阻止跳转(e.preventDefault())

>在表单提交的时候阻止跳转



###拿到input 的输入

首先添加 ref 如下：


```
<input ref={value=>this.comment=value} type="text" className="input" />

```js

上面的ref 意思是指针也就是

```
value=>this.comment=value


```js

是一个箭头函数，其中value 指代当前input 这个节点对应的Object 然后

```
this.comment=value

```js

就是把input 对象赋给一个成员变量，目的是整个class之内，可随处访问



```
 handleSubmit =(e)=>{
         e.preventDefault()
        console.log(this.comment.value)
        >打印你在input输入的内容

        输出console.log(this.comment)
        >打印<input ref={value=>this.comment=value} type="text" className="input" />


    }

```js

在这，如何从form 的输入框拿到字符串 这个技巧我们掌握了。这个一种简单的方式 ，另外通过"受控组件"的形式来取值


###state



先来讨论 render()的本性：

>一旦state 变， render()自动被重新执行

所以，届上的由两条评论变成多个评论


最后 我们还需要提交字符串 吧input 的值清空 input 的字符串。

handleSubmit 添加


```
this.comment.value=" "

```js


但是一个form的input 较多，那么下面的一个更好的方式

```
handleSubmit=()=>{
    this.myForm.reset()
}

```js
<form ref={value=>this.myForm =value} onSubmit ={this.handleSubmit} />
```
