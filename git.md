### 第三章 分支管理
**图文说明：**

`master`分支是一条线，git用`master`指向最新的提交，在用`HEAD`指向`master`，以此才确定当前分支，和提交点。

<img src="master.png">

<br>
**1. 查看分支合并图解**

<img src="branch.png">


<br>
**关于分支的主要命令如下**

* 查看分支

		$ git branch
* 创建`newBranch`分支

		$ git branch newBranch
* 切换`HEAD`指向`newBranch`分支

		$ git checkout newBranch
* 创建+切换分支

		$ git checkout -b newBranck
* 合并某分支到当前分支

		$ git merge newBranch
* 普通删除`newBranch`分支

		$ git branch -d newBranch

* 强行删除`newBranch`分支

		$ git branch -D newBranch

* 查看分支合并状况

		$ git log --graph --pretty=oneline --abbrev-commit

### 9. 藏匿当前未提交的分支

如： 当前在修改自己的分支`dev`,突然项目经理要求修复一个bug-07

解决方法：

1. 藏匿当前`dev`分支的工作状态

		$ git stash
2. 新建一个`bug-07`分支

		$ git branch -b bug-07
3. 修复bug并提交，合并`bug-07`到`master`分支

		$ git commit -m "fix the bug-07"
		$ git checkout master
		$ git merge --no-ff -m "merge  bug-07" bug-07

4. 删除`bug-07`分支

	    $ git branch -d  bug-07
5. 查看当前`stash`

		$ git stash list
6. 恢复`dev`分支的工作状态，并删除stash内容

		$ git stash pop

### 10. 多人协作

* 查看远程库信息

		$ git remote

 * 详细查看远程信息

 		$ git remote -v

 * 推送分支到远程库

		$ git remote origin master

 * 抓取远程分支

 		$ git pull origin master


### 11. 标签管理

 * 创建一个标签，默认为`HEAD`当前分支添加标签

 		$ git tag v1.0

 * 为版本号为`e8b8ef6`添加`v2.0`标签

 		$ git tag v2.0 e8b8ef6

 * 为版本号为`6cb5a9e`添加带有说明的标签，`-a`指定标签名,`-m`指定说明文字

 		$ git tag -a v3.0 -m "version 0.2 released" 6cb5a9e

 * 根据标签查看指定分支

 		$ git show v0.2
 * 查看所有标签

 		$ git tag

 * 删除`v1.0`标签

 		$ git tag -d v1.0

 * 把`v0.9`标签推送到远程

 		$ git push origin v0.9

 * 推送所有尚未推送到远程的本地标签

 		$ git push origin --tags

 * 删除远程标签, 先删除本地标签，再删除远程标签

 		$ git tag -d v0.9
 		$ git push origin :refs/tags/v0.9
