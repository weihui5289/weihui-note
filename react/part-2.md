##Node安装配置
1、安装 nvm

```js
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh | bash
执行这个命令
```

2、安装 node

```js
查看有哪些版本可以安装
nvm ls-remote
安装版本 v5.10.1
nvm install v8.10.1

```

这样就安装好了 node ，同时 npm 页就装好了。执行下面的命令来检查下本地的 node ，npm 版本吧。

```js
node -v
npm -v
```


3、配置 npm

npm 是一个非常强大的包管理工具，可以让我们非常方便的安装、卸载、更新插件包，但是默认的 npm 下载包是从国外的服务器获取，速度很不给力，这里推荐使用淘宝镜像。

```js

npm install -g cnpm --registry=https://registry.npm.taobao.org

```



