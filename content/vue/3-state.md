### 组件内使用数据

现在我们要在 CommentBox 组件内，先显示两条评论（对应 react 的 state）。
参考：https://cn.vuejs.org/v2/guide/
但是，注意，组件内（也就是 .vue 中）使用 data , 要求 data 定义的时候必须是一个函数。使用的时候，要插入到中间

```js
<template>
  <div class="comment-box">
    {{ message }}
  </div>
</template>

<script>
  export default {
    name: 'comment-box',
    data: () => ({
      message: 'Hello Everyone'
    })
  }
</script>
```


### 指令
就是以 v- 打头的那些字符串。

现在我们想渲染一个列表，这个用到的是 v-for 。

参考：https://cn.vuejs.org/v2/guide/list.html

指令是模板的必然产物，特点是对新手亲和，缺点就是没有 JSX 那么直接和强大。这个就是很多高手喜欢 react 的最大原因之一。
