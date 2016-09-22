>#git学习记录

<br>

>## 第一章git分支 - 分支的新建与合并

<br>

>### 新建：

<br>

   >切换分支
   
   * 想要新建一个分支并同时切换到那个分支上，你可以运行一个带有 -b 参数的 git checkout 命令：<br>
   $git checkout -b iss53    
   Switched to a new branch "iss53"<br> 
   它是下面两条命令的简写：<br>
   $ git branch iss53   
   $ git checkout iss53
>新分支指针

   * 你继续在 #53 问题上工作，并且做了一些提交。 在此过程中，iss53 分支在不断的向前推进，因为你已经检出到该分支（也就是说，你的 HEAD 指针指向了 iss53 分支）:<br>
   $ vim index.html<br>
  $ git commit -a -m 'added a new footer [issue 53]'
  
>保存进度（stashing） 和 修补提交（commit amending）我们会在 储藏与清理 中看到关于这两个命令的介绍。 现在，我们假设你已经把你的修改全部提交了，这时你可以切换回 master 分支了:

* $ git checkout master <br>
Switched to branch 'master'

>让我们建立一个针对该紧急问题的分支（hotfix branch），在该分支上工作直到问题解决：

* $ git checkout -b hotfix <br>
Switched to a new branch 'hotfix' <br>
$ vim index.html <br>
$ git commit -a -m 'fixed the broken email address' <br>
[hotfix 1fb7853] fixed the broken email address <br>
 1 file changed, 2 insertions(+)
>### 第二章 分支的合并

* iss53分支的工作成果合并到master分支上：<br>
$ git merge iss53 				 <br>
Updating d17efd8..fec145a        <br>
Fast-forward 					 <br>
 readme.txt |    1 +             <br>
 1 file changed, 1 insertion(+)  <br>
*合并完成后，就可以放心地删除dev分支了： <br>
$ git branch -d dev					<br>
Deleted branch dev (was fec145a).   <br>
* 删除后，查看branch，就只剩下master分支了：<br>
$ git branch  <br>   * master
 
>###总结

查看分支：git branch

创建分支：git branch [name]

切换分支：git checkout [name]

创建+切换分支：git checkout -b [name]

合并某分支到当前分支：git merge [name]

删除分支：git branch -d [name]
>##git分支管理

<br>

>得到当前所有分支的一个列表：

* $ git branch  <br>
  iss53         <br>
  \* master        <br>
  testing       <br>
>查看每一个分支的最后一次提交，可以运行 git branch -v 命令：

* $ git branch -v                            <br>
  iss53   93b412c fix javascript issue       <br>
  \* master  7a98805 Merge branch 'iss53'    <br>
  testing 782fd34 add scott to the author list in the readmes <br>

>要查看哪些分支已经合并到当前分支，可以运行 git branch --merged：

* $ git branch --merged <br>
  iss53                 <br>
\* master               <br>
 
>查看所有包含未合并工作的分支，可以运行 git branch --no-merged：

* $ git branch --no-merged   <br>
  testing                    <br>

>这里显示了其他分支。 因为它包含了还未合并的工作，尝试使用 git branch -d 命令删除它时会失败：

$ git branch -d testing      <br>
error: The branch 'testing' is not fully merged.    <br>
If you are sure you want to delete it, run 'git branch -D testing'. <br>

>##git分支开发工作流

<br>

>长期分支

* 因为 Git 使用简单的三方合并，所以就算在一段较长的时间内，反复把一个分支合并入另一个分支，也不是什么难事。 也就是说，在整个项目开发周期的不同阶段，你可以同时拥有多个开放的分支；你可以定期地把某些特性分支合并入其他分支中。<br>
&nbsp; &nbsp; &nbsp; &nbsp;许多使用 Git 的开发者都喜欢使用这种方式来工作，比如只在 master 分支上保留完全稳定的代码——有可能仅仅是已经发布或即将发布的代码。 他们还有一些名为 develop 或者 next 的平行分支，被用来做后续开发或者测试稳定性——这些分支不必保持绝对稳定，但是一旦达到稳定状态，它们就可以被合并入 master 分支了。 这样，在确保这些已完成的特性分支（短期分支，比如之前的 iss53 分支）能够通过所有测试，并且不会引入更多 bug 之后，就可以合并入主干分支中，等待下一次的发布。

>特性分支

* 特性分支对任何规模的项目都适用。 特性分支是一种短期分支，它被用来实现单一特性或其相关工作。 也许你从来没有在其他的版本控制系统（VCS）上这么做过，因为在那些版本控制系统中创建和合并分支通常很费劲。 然而，在 Git 中一天之内多次创建、使用、合并、删除分支都很常见。

>##git 远程分支

* 远程分支（remote branch）是对远程仓库中的分支的索引。它们是一些无法移动的本地分支；只有在 Git 进行网络交互时才会更新。远程分支就像是书签，提醒着你上次连接远程仓库时上面各分支的位置。我们用 (远程仓库名)/(分支名) 这样的形式表示远程分支。

>推送

* 当你想要公开分享一个分支时，需要将其推送到有写入权限的远程仓库上。 本地的分支并不会自动与远程仓库同步 - 你必须显式地推送想要分享的分支。 这样，你就可以把不愿意分享的内容放到私人分支上，而将需要和别人协作的内容推送到公开分支。<br>
&nbsp; &nbsp; &nbsp; &nbsp;如果希望和别人一起在名为 serverfix 的分支上工作，你可以像推送第一个分支那样推送它。 运行 git push (remote) (branch):
$ git push origin serverfix         					<br>
Counting objects: 24, done.								<br>
Delta compression using up to 8 threads.				<br>
Compressing objects: 100% (15/15), done.				<br>
Writing objects: 100% (24/24), 1.91 KiB | 0 bytes/s, done.  <br>
Total 24 (delta 2), reused 0 (delta 0)					<br>
To https://github.com/schacon/simplegit					<br>
 \* [new branch]      serverfix -> serverfix				<br>
  
>跟踪分支
### 1. 工作区（Working Directory）和版本库（Repository）
<br>
	

**说明：**


* 工作区就是创建仓库的文件夹如（learngit文件夹就是一个工作区）
* 版本库就是工作区的隐藏目录`.git`,版本库中有暂存区（stage/index）和分支（master）
* git add 实际是把文件添加到暂存区， git commit 把暂存区的内容提交到当前分支


### 2.创建版本库

1. 创建git仓库文件夹，名为：`learngit`

		$ mkdir learngit

2. 进入leadngit文件夹

		$ cd learngit
3. 初始化git仓库

		$ git init

### 3. 添加文件
1. 在`leangit`下添加一个`readme.txt`文件，并编辑一些内容

2. 添加到仓库暂存区（）在暂存区 文件会变绿

		$ git add readme.txt
3. 提交readme.txt文件到当前分支, -m "提交说明"(只有进行 git add 后 go commit 命令才有效)

		$ git commit -m "add readme.txt"		

### 4. 修改文件
#### 4.1 当文件在工作区时
1. 查看readme.txt文件内容

		$ cat readme.txt
2. 修改readme.txt文件内容

3. 查看仓库状态

		$ git status

4. 添加到仓库暂存区，并提交到分支

		$ git add readme.txt
		$ git commit -m "modify readme.txt"

#### 4.2 当文件在暂存区时
1. 修改文件内容
2. 添加到仓库暂存区

		$ git add readme.txt
3. 提交到分支

		$ git commit -m "modify readme.txt at the stage"		


### 5. 撤销修改文件（未提交到分支）
#### 5.1 当文件在工作区时
1. 执行撤销命令

		$ git checkout -- readme.txt

#### 5.2 当文件在暂存区时
1. 令文件回到工作区

		$ git reset HEAD readme.txt
2. 执行撤销命令

		$ git checkout -- readme.txt

### 6. 版本控制（无限次后悔）

说明：在Git中，`HEAD`表示当前版本，`HEAD^`表示上一版本 `HEAD^^`表示上上一个版本

1. 查看提交日志输出(完整版)

		$ git log

2. 查看提交日志输出（精简版）

		$ git log --pretty=noline

3. 回到上一版本

		$ git reset --hard HEAD^

4. 回到指定版本（hard 后面添加版本号）

		$ git reset --hard ea34578

5. 查看命令历史

		$ git reflog



### 7. 远程仓库（github）
#### 7.1 添加到远程库
1. 在github上创建一个名为`learngit`的空仓库
2. 在本地`learngit`仓库下运行命令

		$ git remote add origin git@github.com:iphone5solo/learngit.git
3. 把本地内容推送到github远程库上(第一次push 参数带 `-u` 关联远程仓库)

		$ git push -u origin master

注意：如果在git push -u origin master时出现以下错误，证明电脑没有修改远程仓库的公钥，


	Permission denied (publickey).
	fatal: Could not read from remote repository.

	Please make sure you have the correct access rights
	and the repository exists.

解决方法：

1. 在github上点击`Edit profile` --> `SSH and GPG keys` --> `new SSH key` 添加SHH公钥
2. 打开`id_rsa.pub`文件（/Users/iphone5solo/.ssh/id.rsa.pub）
3. 将`id_rsa.pub`文件内容拷贝到key就可以了，title随便填。

#### 7.2 从远程库克隆
1. 在github上创建一个名为`clonegit`的仓库
2. 使用命令克隆仓库

		$  git clone git@github.com:iphone5solo/clonegit

#### 7.3 从远程仓库更新本地仓库（已关联）

		$ git pull origin master
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
