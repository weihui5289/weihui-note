##前言

...
Git 及 Github 在工作学习中非常重要，它不仅仅是一个管理存放代码的仓库，更是一个开源的社区。学习Git及Github的操作是首要技能。 廖雪峰的 Git 教程
额，文档整理的不一定完全准确，请酌情参考。


##基本命令操作

* git init

```js
mkdir demo && cd demo
git init

```

* git clone
如果在 github 上已经有了仓库，可以直接通过 git clone 将项目 clone 到本地。

```js
git clone [仓库地址]
```

* git log
查看提交记录

* git add
`git add` 可以将文件添加到缓存去，获得 Git 的跟踪。

```js
touch a.html
git add a.html

也可以通过加参数，将所有的文件添加到缓存区。下面的三种方式效果相同。
git add .
git add -A
git add *
```

* git status
可以查看当前版本库各个文件的状态。
```js

git status

```

* git commit
`git commit` 将缓存区内容添加到仓库中

```js
git commit -m '版本留言，尽量写的语义话'

```

* git rm
`git rm `命令把一个文件删除，并把它从git的仓库管理系统中移除。

```js
git rm readme.md

```

