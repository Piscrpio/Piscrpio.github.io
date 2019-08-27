---
title: HEXO在新电脑上怎么部署
date: 2017-08-23 16:09:47
categories: web
tags: hexo
---

使用Hexo搭建的博客，在生成的文件里面有一个.gitignore文件。里面列举的文件都是不重要的，也就是说如果你只是拷贝了这一部分的内容，想要在另一台电脑上继续编辑之前的博客是不可能的了，只能重新搭建一次博客。除了.gitignore列举的文件，其他的都是必须的。如果少了一些文件，重新部署的时候会出现不同的情况，就不一一说明了。如果你把所有必须的文件都拷贝了，可以通过下面的指令在另一台电脑上重新部署（在拷贝的新的文件里通过git bash进行操作）：
<!--more-->
```
npm install hexo
npm install
npm install hexo-deployer-git

```

** 记住，因为你不是重新搭建一个Hexo，而是想继续编辑之前的博客，所以不需要用hexo init这条指令。 **
建议去看下 [使用hexo，如果换了电脑怎么更新博客？ - GitHub](https://www.zhihu.com/question/21193762) 这个问题的回答，会更清楚。
