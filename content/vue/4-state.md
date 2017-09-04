### 添加评论
涉及到的知识点：
```js
响应事件，采用： v-on:click 或者 v-on:keypress.enter
定义方法 method
```
### 响应事件
```js
<button v-on:click="addComment"
```
### 添加方法
```js
methods: {
  addComment: function () {

  }
}
```


### 逆序显示评论
我们知道，就是用 [].reverse() 但是，如果我们直接

```js
[Vue warn]: You may have an infinite update loop in a component render function.
```
翻译：Vue 警告：你可能陷入一个无限的在组件 render 函数内的更新循环。

结论就是：不要到 template 中进行数据运算。而要使用
https://cn.vuejs.org/v2/guide/computed.html
也就是使用计算属性。
