---
title: hexo备份
date: 2017-11-24 16:14:48
categories: web
tags: hexo
---

git init
echo "node_modules/" > .gitignore
echo "public/" >> .gitignore
echo ".deploy_git" >> .gitignore
git checkout -b hexo      // git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
git add .
git commit -m "initial commit"
git remote add origin git@github.com:houyazhao/houyazhao.github.io.git

（提示出错信息：fatal: remote origin already exists.
先输入git remote rm origin
再输入git remote add origin git@github.com:houyazhao/houyazhao.github.io.git 就不会报错了！）


git push -u origin hexo


# 恢复

git clone -b hexo --single-branch git@github.com:houyazhao/houyazhao.github.io.git
cd speedoops.github.io.git
cnpm install


在本地对博客进行修改（添加新博文、修改样式等等）后，通过下面的流程进行管理。

1. 依次执行git add .、git commit -m "..."、git push origin hexo指令将改动推送到GitHub（此时当前分支应为hexo）；
2. 然后才执行hexo g -d发布网站到master分支上。
