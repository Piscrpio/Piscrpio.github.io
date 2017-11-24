---
title: gulp入门实战
date: 2017-11-24 16:11:52
categories: web
tags: gulp
---
## gulp新手实战

Gulp 是一个自动化工具，前端开发者可以使用它来处理常见任务：
- 搭建web服务器
- 文件保存时自动重载浏览器
- 使用预处理器如Sass、LESS
- 优化资源，比如压缩CSS、JavaScript、压缩图片


### 实现一个的工作流
- 搭建本地web服务器
- 编译Sass
- 每当保存更改，自动刷新浏览器
- 优化&压缩资源

### 安装gulp
安装Gulp之前你需要先安装Node.js。
安装完node.js之后在终端全局安装Gulp
```
npm install gulp -g
```

### 创建Gulp项目
##### 首先，我们新建一个project文件夹，并在该目录下执行
```
npm init
```
npm init命令会为你创建一个package.json文件，这个文件保存着这个项目相关信息。比如你用到的各种依赖（这里主要是插件）<br>


##### 创建完之后，我们执行下面的命令：<br>
```
npm install gulp --save-dev
```

局部安装Gulp。使用—save-dev，将通知计算机在package.json中添加gulp依赖。<br>
执行完之后，gulp将创建node_modules文件夹，里面有个gulp文件夹。

##### 目录结构
![gulp-for-beginner-structure.png](http://upload-images.jianshu.io/upload_images/3406013-758766fcf826ada8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

app文件夹作为开发目录（所有的源文件都放在这下面），dist文件夹用来存放生产环境下的内容。


##### 现在我们来创建gulpfile.js。

```
var gulp = require('gulp');
var sass = require('gulp-sass');
var browserSync = require('browser-sync');
var useref = require('gulp-useref');
var uglify = require('gulp-uglify');
var gulpIf = require('gulp-if');
var cssnano = require('gulp-cssnano');
var imagemin = require('gulp-imagemin');
var cache = require('gulp-cache');
var del = require('del');
var runSequence = require('run-sequence');

// Basic Gulp task syntax
//gulp.task('hello', function() {
//  console.log('Hello Zell!');
//})

// Development Tasks
// -----------------

// Start browserSync server
gulp.task('browserSync', function() {
  browserSync({
    server: {
      baseDir: 'app'
    }
  })
})

gulp.task('sass', function() {
  return gulp.src('app/scss/**/*.scss') // Gets all files ending with .scss in app/scss and children dirs
    .pipe(sass().on('error', sass.logError)) // Passes it through a gulp-sass, log errors to console
    .pipe(gulp.dest('app/css')) // Outputs it in the css folder
    .pipe(browserSync.reload({ // Reloading with Browser Sync
      stream: true
    }));
})

// Watchers
gulp.task('watch', function() {
  gulp.watch('app/scss/**/*.scss', ['sass']);
  gulp.watch('app/*.html', browserSync.reload);
  gulp.watch('app/js/**/*.js', browserSync.reload);
})

// Optimization Tasks
// ------------------

// Optimizing CSS and JavaScript
gulp.task('useref', function() {

  return gulp.src('app/*.html')
    .pipe(useref())
    .pipe(gulpIf('*.js', uglify()))
    .pipe(gulpIf('*.css', cssnano()))
    .pipe(gulp.dest('dist'));
});

// Optimizing Images
gulp.task('images', function() {
  return gulp.src('app/images/**/*.+(png|jpg|jpeg|gif|svg)')
    // Caching images that ran through imagemin
    .pipe(cache(imagemin({
      interlaced: true,
    })))
    .pipe(gulp.dest('dist/images'))
});

// Copying fonts
gulp.task('fonts', function() {
  return gulp.src('app/fonts/**/*')
    .pipe(gulp.dest('dist/fonts'))
})

// Cleaning
gulp.task('clean', function() {
  return del.sync('dist').then(function(cb) {
    return cache.clearAll(cb);
  });
})

gulp.task('clean:dist', function() {
  return del.sync(['dist/**/*', '!dist/images', '!dist/images/**/*']);
});

// Build Sequences
// ---------------

gulp.task('default', function(callback) {
  runSequence(['sass', 'browserSync'], 'watch',
    callback
  )
})

gulp.task('build', function(callback) {
  runSequence(
    'clean:dist',
    'sass',
    ['useref', 'images', 'fonts'],
    callback
  )
})
```
##### 此项目中gulp的依赖package.json
```
{
  "name": "project",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "browser-sync": "^2.7.12",
    "del": "^2.0.2",
    "gulp": "^3.9.0",
    "gulp-autoprefixer": "^3.1.0",
    "gulp-cache": "^0.4.1",
    "gulp-cssnano": "^2.1.0",
    "gulp-if": "^2.0.0",
    "gulp-imagemin": "^2.3.0",
    "gulp-sass": "^3.0.0",
    "gulp-sourcemaps": "^1.5.2",
    "gulp-uglify": "^1.2.0",
    "gulp-useref": "^3.0.4",
    "run-sequence": "^1.1.2"
  }
}
```


#### Node中的通配符
1. *.scss：*号匹配当前目录任意文件，所以这里*.scss匹配当前目录下所有scss文件
2. **/*.scss：匹配当前目录及其子目录下的所有scss文件。
- !not-me.scss：！号移除匹配的文件，这里将移除not-me.scss
- *.+(scss|sass)：+号后面会跟着圆括号，里面的元素用|分割，匹配多个选项。这里将匹配scss和sass文件。
