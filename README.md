## What is Travis CI?

[Travis CI](https://travis-ci.org/) is a hosted [continuous integration](https://en.wikipedia.org/wiki/Continuous_integration) platform that is free for all open source projects hosted on Github.

With a file called `.travis.yml`, you can trigger automated builds with every change to your repo.

## How to use Travis CI?

1. Sign in to [Travis CI](https://travis-ci.org/auth) with your GitHub account.

1. Go to your [profile page](https://travis-ci.org/profile) and choose a repository to run Travis CI builds.

## Travis CI

### 实验目的

1. 了解持续集成的做法，学会使用 Travis CI。

### 操作步骤

（1）注册 [Github](https://github.com) 的账户。如果你已经注册过，跳过这一步。

（2）访问这个代码库[`github.com/ruanyf/travis-ci-demo`](https://github.com/ruanyf/travis-ci-demo)，点击右上角的`Fork`按钮，将它克隆到你自己的空间里面。

（3）将你`fork`的代码库，克隆到本地。注意，要将下面网址之中的`[your_username]`改成你的 Github 用户名。

```bash
// Linux & Mac
$ git clone git@github.com:[your_username]/travis-ci-demo.git

// Windows
$ git clone https://github.com:[your_username]/travis-ci-demo
```

（4）使用你的 Github 账户，登录 [Travis CI](https://travis-ci.org/auth) 的首页。然后，访问 [Profile](https://travis-ci.org/profile) 页面，选定`travis-ci-demo`代码库运行自动构建。

（5）回到命令行，进入你本地的`travis-ci-demo`目录，切换到`demo01`分支。

```bash
$ cd travis-ci-demo
$ git checkout demo01
```

项目根目录下面有一个`.travis.yml`文件，这是 Travis CI 的配置文件。如果没有这个文件，就不会触发 Travis CI 的自动构建。打开看一下。

```bash
language: node_js
node_js:
  - "node"
```

上面代码指定，使用 Node 完成构建，版本是最新的稳定版。

指定 Node 的版本号也是可以的。

```javascript
language: node_js
node_js:
  - "4.1"
```

上面代码指定使用 Node 4.1 版。

（6）Travis CI 默认依次执行以下九个脚本。

- `before_install`
- `install`
- `before_script`
- `script`
- `after_success` 或者 `after_failure`
- `after_script`
- `before_deploy`（可选）
- `deploy`（可选）
- `after_deploy`（可选）

用户需要用到哪个脚本，就需要提供该脚本的内容。

对于 Node 项目，以下两个脚本有默认值，可以不用自己设定。

```javascript
"install": "npm install",
"script": "npm test"
```

（7）打开当前分支的`package.json`，可以发现它的`test`脚本是一个`lint`命令。

```javascript
"scripts": {
  "test": "jshint hello.js"
},
```

（8）在项目根目录下，新建一个新文件`NewUser.txt`，内容是你的用户名。提交这个文件，就会触发 Travis CI 的自动构建。

```bash
$ git add -A
$ git commit -m 'Testing Travis CI'
$ git push
```

（9）等到 Travis CI 完成自动构建，到页面上[检查](https://travis-ci.org/repositories)构建结果。

（10）切换到`demo02`分支，打开`package.json`，可以看到`test`脚本，现在需要完成两步操作了。

```javascript
  "scripts": {
    "lint": "jshint hello.js hello.test.js",
    "test": "npm run lint && mocha hello.test.js"
  },
```

（11）重复上面第 8 步和第 9 步。

### 练习

1. 修改`hello.js`，让其输出`Hello Node`。并修改测试用例`hello.test.js`，使之能够通过 Travis CI 的自动构建。
