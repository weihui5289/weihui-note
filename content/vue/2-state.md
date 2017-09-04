### VUE-CLI 建立状态   命令行
一个简单的CLI脚手架Vue.js项目。

#### 安装
```js
$ npm install -g vue-cli
```


#### 用法
```js
$ vue init < template-name >  < project-name >
参考下面例子：
$ vue init webpack my-project
```
上述命令从vuejs-templates / webpack中提取模板，提示输入一些信息，并在其中生成项目./my-project/。


### vue构建

使用vue-cli作为您的Vue应用程序和组件的零配置开发工具，查看<font color='red'>[文档](https://github.com/vuejs/vue-cli/blob/master/docs/build.md)</font>


选项中，比较重要的就是选择使用

* Standard ： JS ”标准“ 代码风格
https://standardjs.com/

* Airbnb : Airbnb 公司的代码风格
https://github.com/airbnb/javascript

对于 Peter 来说，二者最大的区别就是，写不写分号，Peter 不喜欢写分号，所以选择 Standard 。


### 路由 vue-router
把历史从 hash 历史，改为 /历史 （标准说法应该叫 history 历史，因为使用 history 这个包来达成的）。
如何启动 history 历史 呢？

```js
mode: history
```


### 充电：Standard 标准的执行
代码报错：
```js
Missing space before value for key 'name'  
  src/router/index.js:13:12
        name:'Home',
```
意思是：在 name 键的值之前，少一个空格。这个不是 js 语法错误，这个是 Standard 代码风格的要求。


**router-link**

```<router-link>``` 组件支持用户在具有路由功能的应用中（点击）导航。 通过 to 属性指定目标地址，默认渲染成带有正确链接的 <a> 标签，可以通过配置 tag 属性生成别的标签.。另外，当目标路由成功激活时，链接元素自动设置一个表示激活的 CSS 类名。


<router-link> 比起写死的 <a href="..."> 会好一些，理由如下：

无论是 HTML5 history 模式还是 hash 模式，它的表现行为一致，所以，当你要切换路由模式，或者在 IE9 降级使用 hash 模式，无须作任何变动。

在 HTML5 history 模式下，router-link 会拦截点击事件，让浏览器不再重新加载页面。

当你在 HTML5 history 模式下使用 base 选项之后，所有的 to 属性都不需要写（基路径）了。

**Props**

```类型: string | Location```



### 添加新的组件

到 Post.vue 里面，添加两个子组件 PostBody.vue CommentBox.vue 。
```js
这里采用：https://cn.vuejs.org/v2/guide/components.html#局部注册
```


### CSS 相关知识
>如果组件内的 CSS ，不希望影响其他组件，那就加上 scoped 属性。
scope 的意思是“作用域”，scoped 意思是”被限制作用域的“
