## webpack基础

webpack是一款强大的模块加载器兼打包工具，它能把各种资源，例如JS（含JSX）、coffee、样式（含less/sass）、图片等都作为模块来使用和处理。官网
接下来我们将一步步熟悉Webpack的使用，并使用它来搭建一套前端工作流。

### 1.初始化项目


-`创建一个项目`

```js
cd webpack-demos && $ mkdir webpack-demos
$ git init
$ touch README.md .gitignore
$ npm init
```


-`编辑.gitignore`

```js
node_modules
*.log*
.idea
```

-`建立src和build两个目录`

```js
// src 目录存放源码，build 目录存放编译打包之后的资源
$ mkdir src build
$ cd src && touch index.js component.js
$ cd ../ && touch index.html
```

-`下载webpack和webpack-dev-server`

```js
# 安装并保存在项目的依赖中
$ npm install --save-dev webpack webpack-dev-server
# 如果想直接在命令行使用webpack或webpack-dev-server命令，请全局安装
$ npm install -g webpack webpack-dev-server
```

-`创建webpack的配置文件`
```js
$ touch webpack.config.js
```

-`进行基本配置`
```js
ar path = require('path');

module.exports = {
    entry: path.resolve(__dirname, 'src/index.js'),
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: 'bundle.js'
    },
};
```

-`执行webpack命令,这里我们用的是项目内安装的webpack`
```js
$ ./node_modules/.bin/webpack
```




#### 2.webpack和webpack-dev-server的基本命令
```js
$ webpack --help
```

-webpack 开发环境下编译
-webpack -p 产品编译及压缩
-webpack --watch 开发环境下持续的监听文件变动来进行编译(非常快!)
-webpack -d 引入 source maps
-webpack --progress 显示构建进度
-webpack --display-error-details 这个很有用，显示打包过程中的出错信息
-webpack --profile 输出性能数据，可以看到每一步的耗时


另外，让我们使用webpack-dev-server来起一个本地服务进行调试,这里任然用的是项目内部的webpack-dev-server

```js
$ ./node_modules/.bin/webpack-dev-server --progress --colors
修改我们的index.html代码
```

```js
<script type="text/javascript" src="/bundle.js"></script>
打开localhost:8080，回车即可。
```

那么执行webpack-dev-server后面的几个参数是什么意思呢？

-webpack-dev-server - 在 localhost:8080 建立一个 Web 服务器
-webpack-dev-server --devtool eval - 为你的代码创建源地址。当有任何报错的时候可以让你更加精确地定位到文件和行号
-webpack-dev-server --progress - 显示合并代码进度
-webpack-dev-server --colors - 命令行中显示颜色
-webpack-dev-server --content-base build - webpack-dev-server服务会默认以当前目录伺服文件，如果设置了content-base的话，服务的根路径则为build目录
-webpack-dev-server --inline 可以自动加上dev-server的管理代码，实现热更新
-webpack-dev-server --hot 开启代码热替换，可以加上HotModuleReplacementPlugin
-webpack-dev-server --port 3000 设置服务端口
关于webpack-dev-server的简单介绍：webpack-dev-server是一个小型的node.js Express服务器,它使用webpack-dev-middleware中间件来为通过webpack打包生成的资源文件提供Web服务。它还有一个通过Socket.IO连接着webpack-dev-server服务器的小型运行时程序。webpack-dev-server发送关于编译状态的消息到客户端，客户端根据消息作出响应。



-`3.devServer`

刚才我们看到，在运行webpack-dev-server的时候，后面带了一串参数，这里我们可以使用devServer字段统一在webpack.config.js文件里面维护。


```js
/* webpack.config.js */
var path = require('path');

module.exports = {
  entry: path.resolve(__dirname, 'src/index.js'),
  output: {
      path: path.resolve(__dirname, 'build'),
      filename: 'bundle.js',
  },
  devServer: {
    publicPath: "/static/",
    stats: { colors: true },
    port: 3000,
    inline: true
  }
};
```


同时，我们可以简化scripts字段的配置了

"scripts": {
    "dev": "./node_modules/.bin/webpack-dev-server"
}
对应的修改index.html文件中的资源引用地址

<script src="/static/bundle.js"></script>
ok, npm run dev即可
