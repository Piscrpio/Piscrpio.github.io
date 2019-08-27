---
title: GIT常用操作命令
date: 2017-11-24 15:02:18
categories: web
tags: git
---
### mkdir learngit   // 创建一个空目录
### cd learngit
### pwd   // 用于显示当前目录
<!--more-->

### git init    // 命令把这个目录变成Git可以管理的仓库
### git add file // 把你的修改放到暂存区
### git status // 查看当前状态，是否有遗漏
### git commit -m "something" // 把文件提交到仓库
### git diff   // 查看difference
### git log   // 命令显示从最近到最远的提交日志
### git log --pretty=oneline     // 输出信息太多的时候
### git reset --hard HEAD^   // 回退上一个版本
在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
### git reset --hard commit-id   // 指定回到未来的某个版本,版本号没必要写全，前几位就可以了，Git会自动去找。
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。<br>
穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。<br>
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。<br>

git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。<br>
每次修改，如果不add到暂存区，那就不会加入到commit中。
### git reflog   //用来记录你的每一次命令
### git checkout -- readme.txt   //把readme.txt文件在工作区的修改全部撤销
- 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
- 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。
- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

### git push -u origin master // 推送到远程仓库
把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
从现在起，只要本地作了提交，就可以通过命令：<br>
git push origin master
- 要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
- 关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
- 此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；


### 文件处理
#### ls   // 读取项目目录
rm test.txt   // 删除文件
- 删除某个文件 git rm test.txt, 然后保存 git commit -m "del", 如果你删错了也可以恢复 git checkout -- test.txt



### 分支相关

#### git checkout -b dev   //创建dev分支，然后切换到dev分支
- git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
- git branch dev
- git checkout dev

#### git branch   ///命令查看当前分支：
#### git checkout master  //切换到master分支：
#### git merge  //命令用于合并指定分支到当前分支。
#### git branch -d dev   //删除分支
- 查看分支：git branch
- 创建分支：git branch <name>
- 把创建的分支推送到远程服务器：git push origin dev
- 删除远程分支 git push origin --delete dev
- 切换分支：git checkout <name>
- 创建+切换分支：git checkout -b <name>
- 合并某分支到当前分支：git merge <name>
- 删除分支：git branch -d <name>
- 强行删除：git branch -D <name> 用于删除一个没有被合并过的分支。
- 查看分支提交详细命令：git log --graph --pretty=oneline --abbrev-commit
- 强制覆盖本地 首先： git fetch --all ，其次：git reset --hard origin/master
- 查看分支合并图：git log --graph
- cat readme.txt //文件内容
- git log --graph --pretty=oneline --abbrev-commit  用带参数的git log也可以看到分支的合并情况：
- 开发一个新feature，最好新建一个分支；
- 如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。
