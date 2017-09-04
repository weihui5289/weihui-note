### 请求 API
### 伪造 API

用 setTimeout 伪造一下 API

### 请求 API 要用 Action
```js
const actions = {
  getAllComments ({ commit }) {
    comment.getComments(comments => {
      console.log('actions', comments)
      commit(types.LOAD_COMMENTS, { comments })
    })
   }
 }
 ```
 配合这个 Action 的 Mutation

 ```js
 const mutations = {

  [types.LOAD_COMMENTS] (state, { comments }) {
    console.log('muations', comments)
    state.all = comments
  }
}
```
