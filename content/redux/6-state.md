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
-connect 连接 store 和组件
-mapStateToProps：把 store 中的数据（一部分）映射为当前组件的 props
map 的意思是“映射”
-State 指的是 store 状态树（ State Tree ），也就是 store 的实际数据
-Porps 就是属性
-Store 中数据很多，当前组件需要的只是一部分，那么选取工作是在 mapStateToProps 中完成的

```js
const mapStateToProps = (state) => ({
  comments: state
});
```

4.connect 完毕之后，PostBody 之中就多了一个属性：this.props.comments

5.只有 connect 不能工作（因为找不着 store），因为 connect 的生效范围是由 <Provider> 组件决定的( Provider 也是一个组件，只有被 Provider 包括起来的组件中才能找得着 store，也就是才能使用 connect)，所以代码中还需要添加

```js
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
