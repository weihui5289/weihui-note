### 使用属性
参考：https://cn.vuejs.org/v2/guide/components.html

#### 静态传入 props
```js
<post-body postId="123">
```
然后到 post-body 组件中，声明一下，就可以直接用了


### 动态绑定变量
```js
data: () => ({
  myId: '2345'
})
```
此时如果还用

```js
<post-body postId="123">
```

这种形式。那么就不能达成我们的预期。

需要写成：

```js
<post-body v-bind:postId="myId"></post-body>
或者：
<post-body :postId="myId"></post-body>
```

### 补充：vue-router 中传递参数
为了把 postId 这部分的相关功能做得完整些，这里我们再插入一段 vue-router 的基础知识：

使用动态路由：https://router.vuejs.org/zh-cn/essentials/dynamic-matching.html

router/index.js 中

```js
{
  path: '/post/:id',
  name: 'Post',
  component: Post
}
```
```js
computed: {
  postId: function () {
    return this.$route.params.id
  }
}
```
