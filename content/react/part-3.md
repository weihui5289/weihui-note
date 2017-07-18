##NPM的使用方法
创建模块，package.json 文件是必不可少的。我们可以使用 NPM 生成 package.json 文件，生成的文件包含了基本的结果。

```js
npm init
```

以上的信息，你需要根据你自己的情况输入。在最后输入 "yes" 后会生成 package.json 文件。同时在这个 json 文件中可以在 script 字段定义我们自己的一些脚本。


###2.使用 npm 命令安装模块

```js

npm install <Module Name>

例如
npm install express --save

```
这时，就会在我们的工程目录下生成一个 node_modules 的文件夹，在里边就会有 express 这个包了。

如果想要用这个包，只需要在需要的地方 require 或者 import 一下就可以了。


####本地安装
将包安装在项目内的 `node_modules` 下，如果没有这个文件夹， npm 会自动创建。可以通过 require() 来引入项目内的包。

```js
npm install express --save  # 版本名和版本号记录在dependencies字段
npm install express --save-dev  # 版本名和版本号记录在devDependencies字段
```








