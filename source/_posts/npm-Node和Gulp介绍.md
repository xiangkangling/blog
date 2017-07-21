---
title: npm -Node和Gulp介绍
date: 2017-07-05 21:29:28
tags:
- 学习
- 笔记
categories:
- js
- web
---



### 流行框架 -工具

#### npm -Node的包管理工具
- node package manager
- [npm官网](https://npmjs.com)
- [淘宝镜像](http://npm.taobao.org/)
- [cnpm](https://github.com/cnpm/cnpm)

#### 安装 node
- 下载`node`的安装包，直接安装

##### 验证是否安装成功
- 1 使用`win + r`键，打开`运行窗口`
- 2 输入`cmd`，敲回车，进入到命令行工具
- 3 输入`node -v`，检测node是否安装成功
- 4 输入`npm -v`，检测 npm

##### 使用淘宝镜像
```
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global
```

#### 使用npm
- 初始化npm配置文件：`npm init`
	+ 简化创建方式：`npm init -y`
- 会生成一个名为：`package.json` 的文件

##### 使用npm下载包
- 命令：`npm install [名称] --save`
	+ 简化命令: `npm i -S jquery`
- 参数`--save` 会修改 `package.json`，添加"dependencies"依赖项
- 注意：会在当前目录中添加一个名为`node_modules`的文件夹
    + 文件夹中存放了，所有下载的包文件
- 下载指定版本号的包：`npm install [包名称]@版本号 --save`


##### package.json
- 作用：npm可以根据该文件，配合`npm install --production`命令，下载配置中的依赖项
- 优势：不用每次都拷贝依赖项，只需要使用package.json即可

##### 移除包
- 命令：`npm remove [名称] --save`
- 作用：删除包文件，并修改`package.json`


#### Gulp 前端自动化构建工具
- [官网](http://www.gulpjs.com)
- [中文网](http://www.gulpjs.com.cn)
- [在线压缩](http://tool.oschina.net)

##### 概述
> Gulp：用自动化构建工具增强你的工作流程！

- 1 易于使用
- 2 高效，利用node.js强大的流（文件流），快速完成构建
- 3 构建工作就像一系列 流管道（水流经过管道）

##### 应用场景
- 项目发布上线之前对项目进行构建
- 自动完成一系列重复的操作

```
js、css、html文件的压缩、混淆、合并、监视文件变化、同步刷新浏览器 等等
Less ==> CSS 或者 Sass ==> CSS
```

##### 安装Gulp命令行
- 1 全局安装 gulp
	+ `npm install --global gulp-cli`
	+ 全局安装的命令只需要执行一次即可！！！
	+ 为了使用 `gulp` 命令！

- 2 作为项目的开发依赖（devDependencies）安装：
	+ `npm install --save-dev gulp`

##### 其他构建工具
- Grunt 、webpack

##### 核心方法
- task() ：gulp中是以任务为单位来实现功能
- src()  ：传入路径参数，获取到要处理的指定文件
- dest() ：指定处理后的文件输出路径
- watch()：监视文件的变化，做出相应的处理

##### 写任务的步骤
- 注意：任务写在 `gulpfile.js` 文件中，这个文件需要我们自己创建

```js
// 1 得到 gulp 模块
var gulp = require("gulp");

// 2 新建任务
gulp.task("js", function() {
	// 使用 src 方法，根据路径 "./app.js" 找到app.js文件
	gulp.src("./app.js")
		// 使用 dest 方法，执行输出路径
		.pipe(gulp.dest("./dist"));
});

// 3 执行： `gulp js` 命令
```

##### 使用gulp的插件
- `gulp-less`：将less转化为css
- `gulp-uglify`：压缩和混淆js代码
- `gulp-concat`：合并js/css文件
- `gulp-cssnano`：压缩css代码
- `gulp-htmlmin`：压缩html代码
	+ [htmlmin文档](https://github.com/kangax/html-minifier)
- `browser-sync`：同步刷新浏览器

- 以上插件都使用：`npm install gulp-[名称] --save-dev` 安装
- 网络不好的情况下，最好是一个个安装，否则，很可能会下载失败

```
npm install --save-dev gulp gulp-uglify gulp-concat gulp-cssnano gulp-htmlmin gulp-less
npm install --save-dev browser-sync
```

#### 参考文章
- [Gulp中文网 -文档](http://www.gulpjs.com.cn)
- [Gulp 入门](https://markpop.github.io/2014/09/17/Gulp%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B/)
- [Gulp+BrowserSync](http://www.browsersync.cn/docs/gulp/)



#### 单独使用 browser-sync
- 作用：更改代码之后自动刷新浏览器

##### 安装
- 命令：`npm install browser-sync -g` 全局安装

##### 监视
- 命令：`browser-sync start --server --files "index.html"`
- 监视单个文件：`--files "index.html"`
- 监视多个文件：`--files "index.html, test.css"`
- 监视目录文件：`--files "./css/*.css"`
- 监视所有文件：`--files "*.*"`

##### 优势
- 动态重新加载样式文件，而不是刷新页面，避免繁琐的操作
- 前提：样式放到一个单独的css文件中

##### 其他应用
- 管理地址：`UI: http://localhost:3001`
- 多浏览器同步测试

```
1 同步事件触发
2 同步浏览器滚动
3 同步文本框内容
```




