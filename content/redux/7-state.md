### 添加点赞功能

目前 这个组件PostBody 组件中只显示评论，现在我们在添加一个点赞功能

```js
<div className="likes-num num" onClick={this.handleClick}>{newArr.likes}人 赞</div>
```


### Store 中存入多类数据

#### 在去创建一个 likeReducer ，然后 reducers/index.js 中这样写

```js
import likeReducer from './like'
import commentReducer from './comment'
import { combineReducers } from 'redux'


const rootReducer = combineReducers({
  comments: commentReducer,
  likes: likeReducer
})


export default rootReducer

```
这样上面的 comments 和 likes 最终对应了 store.getState() 输出的状态数的对象的两个key




### 显示“0赞”
到 PostBody.js 中，有

```js
const mapStateToProps = (state) => ({
  comments: state

})
```
当然一定注意`comments:state`引用完`import { combineReducers } from 'redux'`

```js
const mapStateToProps = (state) => ({
  comments: state.comments
})
```

并且紧跟着的点赞likes

```js
const mapStateToProps = (state) => ({
  comments: state.comments,
  likes: state.likes
})

```
