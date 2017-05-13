title: Git工作流
date: 2016-03-25 22:42:23
tags: Git
permalink: git-workflow
---

上学期组队做项目，由于队友们都不熟悉 Git 以及 GitHub 的操作，特意写了一份 Git 工作流手册。
这学期有时间，整理了下。

<!-- more -->

## 项目初始
打开 git shell ，cd 进入一个文件夹内，这个文件夹下将会产生新的子文件夹，放置 github 上的代码  
之后执行 `git clone https://github.com/nicktogo/NiceLife.git`
> NiceLife 目前是一个私有仓库，作为我的 .Net 课程项目正在开发中，所以你并不能 clone 下来。  
你可以在 github 上创建自己的一个，方法请查阅：[Create a new repo](https://help.github.com/articles/creating-a-new-repository/).


执行完上述命令后，会把整个代码拉下来，在生成的 `/d/Developer/NiceLife` 文件夹里。

如：  

![](http://i.imgur.com/WpoffP8.png)  

## 开发  
+ 进入 `NiceLife` 文件夹
+ 右键 `git bash`  

	![](http://i.imgur.com/vBYrMQn.png)  
    
	可以看到当前我们在 `master` 分支上，这个是我们的主分支，所有最终代码都会在这个分支上。   
	**注意：** 不要直接在 `master` 开发
+ 新建分支 ( `branch` )
	+ `git branch branchname`
	新建分支
    
	+ `git checkout branchname`
	切换到刚刚新建的分支上
    
	+ `git checkout -b branch_name`
	新建一个分支，并且切换到这个分支上
      
	此时，新分支的代码和当前分支的代码是一样的(我现在的当前分支就是 `master` )
	
	![](http://i.imgur.com/MPxhGXO.png)
+ 写代码  
    `README.md` 中原本只有一句：An Universal Windows Platform app for managing your daily life。
	现在，我在这句之前加了下面一句话：  
	`This is a best practice for git` 
+ 提交
	+ `git status` 查看状态  
	![](http://i.imgur.com/0Ebr4BF.png)  
    
	`modified` 显示我刚刚修改过的文件  
	常见的还有 `new` 表示是新添加的文件，`deleted` 表示是被删除的文件  

	+ `git add .` 或 `git add -u`  
	前一个是把所有已修改或新的文件加入暂存区  
	后一个是仅仅把已修改的添加到暂存区，那为什么有了第一个还有第二个？==   
	因为有时候文件夹里出现的新文件不是你创建的类啊什么的，而是一些无关文件，例如 `log` 、`配置文件（里面有用户名密码什么的）` 什么的，你不想要 `git` 也接管这些东西，以免到时候上传到远程仓库的时候被人发现用户名密码，`log` 什么的也不要让它接管，要不然会使得远程仓库看起来很乱，远程仓库一般只有：**代码、资源文件、LICENSE、README.md**等  
	所以如果没有新的**代码、资源文件**的时候，我们一般只用 `git add -u`  
	如果你确定新增加的只有代码、资源文件，可以直接 `git add .`  
	![](http://7vzny7.com1.z0.glb.clouddn.com/%E6%8D%95%E8%8E%B7.PNG?attname=)  
  
	+ `git commit -m "msg"`  
	`msg` 简短地说明这次代码变动，要有意义。  
	![](http://i.imgur.com/SkuQExs.png)  
      
	会打印出改动

	+ `git push origin HEAD:[之前的分支名]`  
	将代码推送到远程仓库，`origin` 指的就是那个远程仓库的地址  
	`HEAD:[branch name]`，表示把当前分支推送到远程仓库相同的分支上，远程仓库上没有的话，就会新建一个， `*[new branch]` 就表示远程仓库新建了一个分支  
	一般本地仓库和远程仓库对应的分支名相同，方便一一对应，不过不同名也是可以的
	![](http://i.imgur.com/3uB1aZC.png)

	![](http://i.imgur.com/beeZiTM.png)  
	看，GitHub已经发现我推了一个新分支上去了  
	切换到这个分支上去看看 `README.md`是不是真的变了  
	![](http://i.imgur.com/j0I9uEH.png)  
	  
	呃，忘记换行了，总之，就是 `README.md` 真的发生了变化
	![](http://i.imgur.com/TW2xMm4.png)  
	
	但是切换到 `master` 分支，`readme` 没变化  
	![](http://i.imgur.com/B6tbXY8.png)  
	
	说明这两个分支各自有自己的代码，但是我们不是协同开发吗，自己写自己的，有个蛋用啊！

	+ `pull request`  
	合并请求（好像叫做拉取请求更合适）  
      
	请求 `master` 将 `develop/nick-test` 的代码拉过去，合并掉，这样后者的代码变化也会发生在前者上，这个要在 `GitHub` 上操作了

	![](http://i.imgur.com/lRgweNf.png)          
      
	左边是接受新代码的分支，右边是要被合并的分支，还可以写一写为什么要发起这次合并请求，搞定后右下角~  
	![](http://i.imgur.com/9JJ8Zu1.png)  
      
	其实继续往下拉还能看到之前 `git commit` 时候的详情，`README.md` 里有个 `+` 开头的，就是我新增的代码 
	![](http://i.imgur.com/ujg9loD.png)

	+ `master` 处理合并请求
	![](http://i.imgur.com/1b0ffz5.png)

	不过先别急着合并，负责合并的人，得先看看有哪些改动，常说的代码审查。
	![](http://i.imgur.com/lLf3h91.png)
	
	觉得没问题之后，就可以合并了，完成后，可以看到 `master` 的 `README.md` 也变了。
	![](http://i.imgur.com/sEJxi3u.png)

	+ `git fetch origin`  
	更新本地仓库的代码，前面的改动都是只在远程仓库里的，本地不会自动跟进的，要手动取回代码
	![](http://i.imgur.com/4xBmjfT.png)  
    
	`master` 对应的远程分支有更新！但是我们这个时候看本地仓库里 `master` 的 `README.md` 还是原来的样子，是没有新增的那句话的！  
	![](http://i.imgur.com/akskMLr.png)

	+ `git rebase origin/master`  
	变基（奇奇怪怪的翻译 233）  
	让新代码能够应用到本地的当前分支上，我这里希望本地的 `master` 能够有远程 `master`的新代码，就之前先切换回 `master` （git checkout master） 分支上了，  
	![](http://i.imgur.com/C8ZRtJ9.png)

	`rebase` 时的当前分支也可以是其他分支，假设，在还没有 `rebase` 之前，有一个分支基于 `master` 新建出来了，叫做 `test2`, 它的代码和以前的 `master` 是一样的，也没有我新加的那句话，现在我想让它也更新，可以：  
	`git checkout test2`  
	`git rebase origin/master`

	**Tip**  
	一般，我们在自己的分支上 *写代码* 那一步时，也有很多人在同时开发，远程仓库的`master` 上可能通过了很多 `pull request`， 这样我们自己的分支的代码其实就变落后了。
	所以，*写代码* 那一步的时候，可以常常 `fetch` 一下，有输出，说明远程库有新东西，输出里面是更新的分支名，发现有 `master` 的话，就可以 `rebase` 了，保持自己代码和 `master` 最新 