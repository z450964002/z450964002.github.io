---
layout: post
title:  "欢迎观看我的笔记!"
date:   2019-11-11 14:20:20
categories: 个人笔记
tags: featured
image: /assets/article_images/2014-08-29-welcome-to-jekyll/desktop.JPG
---
## git是什么
  + git是目前世界上最好的分布式版本管理器。
  + 版本系统就是能够记录每次的文件改动，可以回滚到之前的版本的神器。
  + git是linux觉得手动管理太麻烦，而且别人的还得要钱，于是他就自己用ｃ语言写了一个git。而且可以通过github社区免费使用。
----------------------



## 集中式与分布式的区别
  + 集中式需要联网下才能工作，并且此方式十分慢，想要修改需要单独把要修改的东西下载到本机上，修改完成在上传回总服务器。
  + 分布式可以每个人都单独下个完整的库，并且通过ssh协议，下载速度很快。修改完成后，可以互相推送，彼此都能看到修改的内容。如果大家统一放在一个主机里，提供给大家修正，会更加方便。而且git的分支管理也是优秀。
----------------------



## 安装git
  + 在ubuntu上安装git只需要输入命令：sudo apt-get install git 就可以直接完成。
  + 其他linux版本需要在git官网下载源码，然后解压，依次输入　`./config`  `make`  `sudo make install`
  + Mac OX x 安装是苹果的安装，方法一，通过homebrew安装git。
  + 从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装。
  + windows安装git，可以从git官网直接下载安装程序，默认选项安装。安装完成后，在开始菜单找到Git-->Git Bash, 会弹出个命令窗口，安装完成后，需要最后的设置，输入：git config --global user.name "Your Name"   git config --global user.email "email@example.com"
----------------------



## 创建版本库
  + `mkdir name`    创建个本地目录，要选好合适的位置
  + `cd name`     　进入这个文件里
  + `git init`　  　把他初始化，变成可管理的仓库首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支：
  + 如果是windows最好不要用记事本写，可以下载notepad++代替。
  + `vim name.txt`          　写个文件
  + `git add name.txt`        添加到仓库缓存区里
  + `git commit -m "注释"`　　提交到当前分支里，留个注释
-----------------------




## 版本回退
  + `git status` 　　查看仓库当前的状态，看看有什么没有处理的。
  + `git diff`       查看做了什么操作。首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支：
  + `git log`        会显示每一次的提交记录，　也可以用`--pretty=oneline可以简化信息`。
  + `git reset --hard HEAD^`     可以回退到上一个版本，多个`^`就可以多退一次。
  + `git reset --hard 版本号`　　可以跳转版本，比如回到最新的。
  + `git reflog`     可以查看命令历史，在看要去哪个版本。
---------------------




## 工作区和缓存区
　+ 工作区　就是电脑的本地文件，
　+ 版本库　是在工作区里的一个隐藏目录，是属于git的版本库。里面有着自动的第一个分支master。
　+ 要把每次的修改都通过add添加到暂存区，然后在commit提交上。
----------------------




## 撤销修改
  + `git checkout -- readme.txt`  在提交前撤销 一定要加 --　否则会执行跳转分支的命令。
  + 已经提交了add，在commit之前发现了问题，需要先回退版本:git reset HEAD readme.txt 回到新版本的文件，再用git status查看，已经来到了，没add之前的时候，这次在进行丢弃工作区操作。
----------------------



## 远程仓库
  + 先创建个ssh key 在用户主目录下，然后看看有没有`id_rsa`,`id_rsa.pub`，如果有，就跳过。
  + 如果没有，`ssh-keygen -t rsa -C "youremail@example.com"`邮箱换成自己的，然后回车，默认后面的选项，密码看个人需求。`id_isa.pub`是公钥，可以告诉别人。
  + 登录GitHub，进入个人设置里的ssh秘钥里面，添加自己的公钥
  + 然后在git里面新建个库，然后在本地里输入以下命令：`git remote add origin git@github.com:z450964002/learngit.git` origin是远程库的名字，可以更改 
  + 下一步，把本地的内容推送到远程库上`git push -u origin master`由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
  + 第一次使用git的clone 或者 push　命令连接github的时候，会得到警告 yes就行。
  + `git clone git@github.com:z45096402/learngit.git`用来克隆库。
---------------------




## 分支管理
  + `git checkout -b dev`  创建新的分支
  + `git branch`  查看所有的分支，前面带\*的是当前分支。
  + `git checkout dev` 　切换分支。
  + `git merge dev`   回到mester分支后，合并两个分支。
  + `git branch -d dev`  删除分支。
---------------------




## 解决冲突
  + 在两个分支都提交后会发生内容冲突，这时候需要手动解决冲突，先用`git status`看看冲突的文件，然后`cat 文件.txt`回出现，  Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，修改后保存。
  + `git log --pretty=oneline --abbrev-commit`可以查看到分支的情况。
  + `git merge --no-ff -m "merge with no-ff" dev`  合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

  + 修改bug时要创建个新的分支，用来改bug 如果当前的工作还没有提交，还是没有办法提交的情况下，先储藏起来，`git stash` ,要先确定在哪个分支上修复bug就从哪个上面建立新的临时分支，把bug修改后，提交。在切回之前的分支，把他合并 最后删除临时分支  在切回之前工作的分支  会发现刚才存的没了，用`git stash list`看看在哪。 用`git stash pop`恢复。删除的同时会把stash的内容也删掉。
  + 为了方便操作，Git专门提供了一个cherry-pick命令，让我们能复制一个特定的提交到当前分支`git cherry-pick 4c805e2`。
  + 没有合并的分支用`git branch -D feature-vulcan`  强力删除分支命令。
------------------




## 多人协作
  + `git remote`  查看远程库的信息。
  + `git remote -v` 显示更加详细的信息。
  + 要在一样的分支上开发，就必须创建远程origin的一样的分支到本地，用这个命令创建本地一样的分支`git checkout -b dev origin/dev`。
  + 如果两人修改了一样的，冲突了，需要用`git pull`把最新的提交从origin/dev抓下来。要先指定本地dev分支与远程origin/dev分支的链接 `git branch --set-upstream-to=origin/dev dev`  在重新`git pull` 抓下来。
  + `git rebase`  rebase操作前后，最终的提交内容是一致的，但是，我们本地的commit修改内容已经变化。
----------------------




## 标签管理
  + `git tag v1.0`  在需要打上标签的分支打上新标签。
  + `git tag`  查看标签。
  + `git tag -a <tagname> -m "blablabla..."`   可以指定标签信息。
  + `git push origin <tagname>`   可以推送一个本地标签。
  + `git push origin --tags`      可以推送全部未推送过的本地标签。
  + `1git tag -d <tagname>`       可以删除一个本地标签。
  + `git push origin :refs/tags/<tagname>`     可以删除一个远程标签。
-----------------




## 忽略特殊文件
  + 忽略某些文件时，需要编写`.gitignore`文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。
  + 不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore。
  + 忽略文件的原则是：

   1. 忽略操作系统自动生成的文件，比如缩略图等；
   2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
   3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。
  + .gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理。
  + z450964002.github.io
