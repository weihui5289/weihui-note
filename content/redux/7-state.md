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



## 接着执行下面的一系列操作

1.先把文件夹变下仓库
```js
cd my-note
git init
git add -A
git commit -m"msg"
git remote add origin git@github.com:happypeter/peter-note.git
git push -u origin master
```

2.为了部署方便，我们把我们的 my-note 的内容结构稍微调整一下，把原有的所有的笔记都放到 content 文件夹中，也就是有这样的目录结构

```
把要写的文件夹放在content里面

```

```js
cd my-note
cd content
ls
README.md  SUMMARY.md redux
```

为何要把内容都统一放到 content 文件夹呢？答案就是，托管到 github 上的内容，其实是一个编译后 的内容，而不是原始内容。现在我们把原始内容都放到 content 文件夹中，未来会把编译输出内容放到 my-note/gh-pages 文件夹中。
