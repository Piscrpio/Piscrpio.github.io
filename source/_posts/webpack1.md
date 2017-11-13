---
title: webpack1
date: 2017-08-02 11:16:48
categories: web
tags: [webpack,前端自动化工具]
---


# webpack 学习

## 正式使用Webpack前的准备

### 一、创建一个package.json文件，这是一个标准的npm说明文件，里面蕴含了丰富的信息，包括当前项目的依赖模块，自定义的脚本任务等等。在终端中使用npm init命令可以自动创建这个package.json文件

```
npm init
```

### 二、 package.json文件已经就绪，在本项目中安装Webpack作为依赖包

```
// 安装Webpack
npm install --save-dev webpack
```

### 三 、创建一个index.html文件

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>demo1</title>
		<script type="text/javascript" src="bundle.js"></script>
	</head>
	<body>
	</body>
</html>
```
### 四、创建一个main.js文件
```
document.write('<h1>Hello World</h1>');
```

### 五、 配置webpack.config.js

```
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  }
};
```
### 六、 构建文件

```
webpack
```

### 一些命令行选项你应该知道。
- webpack – 构建文件
- webpack -p – 发布
- webpack --watch – 监听项目
- webpack -d – 包含 source maps方便调试
- webpack --colors – 让打包界面更好看
