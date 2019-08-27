---
title: webpack实战
date: 2017-11-24 16:25:33
categories: web
tags: webpack
---
创建个名为webpack-your-bags的文件夹


npm init -y
npm install jquery --save
npm install webpack --save-dev 


<!--more-->

--save和--save-dev的区别
-save-dev是指将包信息添加到devDependencies，表示你开发时依赖的包裹。
-save是指将包信息添加到dependencies，表示你发布时依赖的包裹。 
 

创建一个app入口
路径：webpack-your-bags/src/index.js
var $ = require('jquery');
$('body').html('Hello');


创建webpack的配置文件webpack.config.js，webpack.config.js是javascript，需要导出(export) 一个对象(object)
路径：webpack-your-bags/webpack.config.js

var path = require("path");//用于处理目录的对象，提高开发效率（__dirname需要引入path后才可以使用）
var ROOT_PATH = path.resolve(__dirname);//获取当前整个模块文件所在目录的完整绝对路径
var BUILDS_PATH = path.resolve(ROOT_PATH, "builds");//获取我们的builds目录完整绝对路径
module.exports = {
    entry: './src',
    output: {
        path: BUILDS_PATH,
        filename: 'bundle.js',
    },
};





再创建相应的 index.html
路径：webpack-your-bags/index.html

<!DOCTYPE html>
<html>
<body>
    <h1>My title</h1>
    <a>Click me</a>
    <script src="builds/bundle.js"></script>
</body>
</html>

执行webpack，如果一切正常，会看见一个信息告诉我们正确地编译了bundle.js


因为有些浏览器还不支持ES6，所以需要babel来为我们把ES6转为浏览器支持的ES5 ，我们先加入babel的加载器（loader）。

npm install babel-loader --save-dev



我们也得安装babel本身，因为现在我们这个例子加载器不会自动安装它们，因此我们需要装babel-core这个包和它的预设 es2015（也就是在代码被执行前执行的转换器版本）:


npm install babel-core babel-preset-es2015 --save-dev


我们现在创建 .babelrc 文件，告诉babel用哪个预设，这是一个json文件告诉babel在你的代码上执行哪种转换器，现在我们告诉它用es2015：
路径：webpack-your-bags/.babelrc

{
"presets": ["es2015"] 
}


var path = require("path");//用于处理目录的对象，提高开发效率（__dirname需要引入path后才可以使用）
var ROOT_PATH = path.resolve(__dirname);//获取当前整个模块文件所在目录的完整绝对路径
var BUILDS_PATH = path.resolve(ROOT_PATH, "builds");//获取我们的builds目录完整绝对路径
var SRC_PATH = path.resolve(ROOT_PATH, "src");//获取到我们的资源目录src的完整路径
module.exports = {
    entry: './src',
    output: {
        path: BUILDS_PATH,
        filename: 'bundle.js',
    },
    module: {
        loaders: [{
            test: /\.js/,
            loader: 'babel-loader',
            include: SRC_PATH,
        }],
    }
};

用一个非常轻量的模板包Mustache（前后端分离的上古框架，了解就好）
npm install mustache --save
npm install css-loader style-loader html-loader sass-loader node-sass --save-dev










