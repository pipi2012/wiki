---
title: "git-命令"
layout: page
date: 2016-01-27 00:00
---

##配置与初始化
###配置全局username，useremail 
	$ git config --global user.name "your user name"
	$ git config --global user.email "your email name"

###创建版本库（初始化仓库）
	$ cd gitdir
	$ git init

##git分区
###三大分区
	working tree--工作区  
	index file--索引文件（暂存区）  
	HEAD（specified tree）--提交后仓库  

###不同区文件差别比较
	git diff    //working tree与index file差别
	git diff --cached   //查看index file与commit差别
	git diff HEAD  //查看working tree和commit差别

##本地仓库操作
###工作区文件添加索引区index（暂存区stage）
	$ git add <file>

###索引区index（暂存区stage）文件commit到仓库
	$ git commit -m "commit log message"

###查看git库状态 Show the working tree status
	$ git status

###查看commit版本记录
	$ git reflog

###重置head版本/版本回退
	$ git reflog
	$ git reset --hard 版本号

###单步版本回退
	$ git reset --hard HEAD^  //一步回退
	$ git reset --hard HEAD^^  //两步回退
	$ git reset --hard HEAD^^^  //三步回退
	$ git reset --hard HEAD~100  //一百步回退

###工作区修改文件撤销
	git checkout -- <file>  //工作区检出文件
	1）file自动修改后，还没有放到暂存区，使用撤销修改就回到和版本库一模一样的状态。
	2）file修改后已经放入暂存区了，接着又作了修改，撤销修改就回到添加暂存区后的状态。

###撤销重置
	git reset --hard HEAD <file>  //仅commit区回退
	git reset HEAD <file>  //仅commit区和暂存区回退，暂存区未提交文件清空，暂存区撤销到和已提交HEAD版本相同
	等价于  git reset --mixed HEAD <file>
	git reset --hard HEAD <file>  //工作区和暂存区 均会重置到已提交的HEAD版本

###版本回退
	1）如果知道要删掉那些内容的话，直接手动更改去掉那些需要的文件，然后add添加到暂存区，最后commit掉。
	2）可以按以前的方法直接恢复到上一个版本。使用 git reset  --hard HEAD^

##远程仓库操作
###添加关联远程仓库
####1）先有本地仓库，再有远程仓库
	git remote add origin https://github.com/username/repos.git
	git push -u origin master //把本地库的内容推送到远程 -u参数：会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令
	git push origin master //把本地库的内容推送到远程，关联之后操作

####2）先有远程仓库，再有本地仓库
	建立远程仓库
	git clone https://github.com/username/repos.git  //克隆远程仓库到本地仓库

###查看远程库信息
	git remote //查看远程库的信息
	git remote –v //查看远程库的详细信息

###推送分支
	$ git push <远程主机名> <本地分支名>:<远程分支名>

	省略远程分支名，则表示将本地分支推送与之存在”追踪关系”的远程分支(通常两者同名)，如果该远程分支不存在，则会被新建
	$ git push <远程主机名> <本地分支名>
	$ git push origin master

	省略本地分支名，则表示删除指定的远程分支，等同于推送一个空的本地分支到远程分支。
	$ git push <远程主机名> :<远程分支名>
	$ git push origin :master
	等同于
	$ git push origin --delete master

	如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。
	$ git push origin
	如果当前分支只有一个追踪分支，那么主机名都可以省略。
	$ git push

###推送策略
	master分支是主分支，因此要时刻与远程同步。
	一些修复bug分支不需要推送到远程去，可以先合并到主分支上，然后把主分支master推送到远程去。

###拉取分支
	git pull命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并
	$ git pull <远程主机名> <远程分支名>:<本地分支名>

	$ git pull origin next:master  //取回origin主机的next分支，与本地的master分支合并
	$ git pull origin next   //远程分支是与当前分支合并，则冒号后面的部分可以省略

###手动建立追踪关系
	$ git branch --set-upstream master origin/next   //指定master分支追踪origin/next分支

	$ git pull origin  //如果当前分支与远程分支存在追踪关系，git pull就可以省略远程分支名

##分支操作
###创建与合并分支
	git branch  //查看分区
	git checkout -b new_branch  //创建并切换到新分支new_branch
	等价于
	git branch new_branch   //创建新分区new_branch
	git checkout branch  //切换分区branch

###git branch系列操作
	git branch  //不带参数：查看本地已经存在的分支，并且在当前分支的前面加“*”号标记
	git branch -r //列出远程分支
	git branch -a //列出本地分支和远程分支
	git branch new_branch //创建一个新的本地分支，需要注意，此处只是创建分支，不进行分支切换
	git branch -m | -M oldbranch newbranch //重命名分支
	git branch -d | -D branchname //删除branchname分支
	git branch -d -r branchname //删除远程branchname分支

###分支合并
	git merge branch_x //合并指定分支branch_x到当前分支上

###分支策略：
	1)master主分支应该是非常稳定的，也就是用来发布新版本，一般情况下不允许主分支上干活
	2)干活一般情况下在新建的dev分支上干活，干完后，dev分支代码稳定后可以合并到主分支master上来。

##其他
	git stash  //把当前工作现场
	git stash list  //查看stash列表
	stash回复
	1）git stash apply恢复，恢复后，stash内容并不删除，你需要使用命令git stash drop来删除。
	2）另一种方式是使用git stash pop,恢复的同时把stash内容也删除了。

\------------
> 文章修改记录  
> add time 2016-01-27
