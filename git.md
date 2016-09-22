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