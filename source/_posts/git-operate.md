---
title: git_operate
date: 2022-02-21 12:42:15
tags: 编码工具
---
# Git基础操作指南
> 本教程是记录自己对git基础操作的一些理解

>简介：Git是一款免费、开源的分布式版本控制系统，而github是一个远端仓库，通过git可以对github仓库进行管理，同时方便进行团队合作，共同开发项目

<!--more-->
* git status 查询当前文件夹git仓库状态，该命令比较常用，例如可以查看当前文件夹是否初始化 以及 提交历史信息
* git init 初始化仓库，会在本地文件夹下生成一个 .git 文件

* git add 将文件加入到**本地暂存区**，保存本地修改
* `git commit -m 提交描述信息` 将本地暂存区中的所有文件 上传到与本地绑定的远端仓库中
* git log 查询所有的commit信息
* 新建分支：
    * git branch 分支名 创建一个‘分支名`的分支
    * git branch 可以查询当前所有分支
* git checkout 分支  我们的所有操作都是基于分支的，在不同分支间进行切换需要用到此命令
* git branch -b 分支  在创建新分支的同时切换到该分支，一次到位
* 删除分支：
    * git branch -d 分支  当某一分支创建错误，或者该分支所有代码已经合并到master分支，此时该分支已失去价值，可通过此命令删除
    * git branch -D 分支  该命令是强制删除指定分支，场景为：需要删除某一分支，但此时该分支并未合并入主分支，执行上一命令会提示还有分支未合并，可用该命令强制删除

* 打标签：对于程序开发中会有 v.1 v.n 的区别，此时可以给对应的提交代码打标签
    * git tag 标签名
    * git tag  则可以查询历史tag记录
> 同理，在打完标签以后，可以通过标签回退程序 如：git checkout 标签
*** 
## github远端相关操作

>在电脑本地配置好Git环境后，我们就可以从远端仓库pull代码了，但是还不能向远端仓库push代码，因为我们需要将本机电脑同远端仓库建立联系，这时需要用到SSH：

>那么什么是 SSH 呢？ 简单点说，SSH是一种网络协议，用于计算机之间的加密登录。目前是每一台 Linux 电脑的标准配置。而大多数 Git 服务器都会选择使用 SSH 公钥来进行授权，所以想要在 GitHub 提交代码的第一步就是要先添加 SSH key 配置。

* 通过SSH与远端仓库建立联系：Linux 与 Mac 都是默认安装了 SSH ，而 Windows 系统安装了 Git Bash 应该也是带了 SSH的。 在终端输入 ` ssh-keygen -t rsa`  
    * 就是指定 rsa 算法生成密钥，接着连续三个回车键（不需要输入密码），然后就会生成两个文件 id_rsa 和 id_rsa.pub ，而 id_rsa 是密钥，id_rsa.pub 就是公钥。这两文件默认分别在如下目录里生成：向GitHub 提交代码
    * Linux/Mac 系统 在 ~/.ssh 下，win系统在 /c/Documents and Settings/username/.ssh 下，都是隐藏文件。
    * 把 id_rsa.pub 的内容添加到 GitHub 上，这样你本地的 id_rsa 密钥跟 GitHub上的 id_rsa.pub 公钥进行配对，授权成功才可以提交代码
* pull/push 代码：
    * ‘git pull 远程主机名称 远程分支名称：本地分支名称`  从远端仓库拉下来到本地分支
    * `git push 远程主机名称 本地分支名称：远程分支名称`  将本地分支代码推到远程分支上去
    >一般来说我们远程分支名称与本地分支名称保持一致，便捷些
    * **一般为了防止产生冲突，我们强调先pull再push**
    * 删除远程某分支：`git push 远程主机名  ：远程分支` 原理是向远端分支提交一个空的分支覆盖掉，就相当于删除了该远端分支
* 上面提到的远程主机名，即我们对远程仓库的命名，如果不指定则默认 **origin** ,可以通过以下三种方式修改远程主机名：
    1. 克隆仓库时：`git clone -o 远程主机名 仓库网址 指定本地生成文件夹名称`
    >克隆仓库会在本地生成指定名称的文件夹，该文件夹已经初始化完毕
    2. 给已经初始化(git init)后的文件夹添加远程仓库： `git remote add 远程主机名 仓库网址`
    3. 直接更名：`git remote rename 原主机名 新主机名` 
    > git remote 系列命令是对远程主机进行的操作，下面会有详细讲解

* 远程仓库网址命名规则：
    * https: `https://github.com/用户名/项目名.git`
    * ssh: `git@github.com:用户名/项目名.git` 
    > .git 可以省略

* git信息的全局配置 ：`git config --glob xxx`
    * git config —global user.name "stormzhang"
    * git config —global user.email "stormzhang.dev@gmail.com"
    * **简化命令**：`git config --glob alias.别名 原来命令`
        * 例:git config --global alias.co checkout # 别名
    > 一个比较屌的命令，用于美化日志查询 `git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"`

* 为了便于管理，Git要求每个远程主机都必须指定一个主机名，git remote 系列命令就用于对远程主机进行操作：
    * `git remote` 用于查看与该文件夹关联的所有远程主机名
    * `git remote` 同时查看主机名及网址
    * `git remote show 主机名` 列出所有关联主机的详细信息
    * `git remote rm 主机名` 用于删除远程主机
    * 还有上面提到的若干

* 查看文件改动：`git diff` 直接输入 git diff 只能比较当前文件和暂存区文件差异
    * git diff <$id1> <$id2> # 比较两次提交之间的差异
    * git diff <branch1>..<branch2> # 在两个分支之间比较
    * git diff --staged # 比较暂存区和版本库差异
    
* stash 中文释义：暂存区
>对于这个命令向来大家是比较模糊的，不太清楚它的使用场景
设想一个场景，假设我们正在一个新的分支做新的功能，这个时候突然有一个紧急的bug需要
修复，而且修复完之后需要立即发布。当然你说我先把刚写的一点代码进行提交不就行了
么？这样理论上当然是ok的，但是这会产品垃圾commit，原则上我们每次的commit都要有实
际的意义，你的代码只是刚写了一半，还没有什么实际的意义是不建议就这样commit的，那
么有没有一种比较好的办法，可以让我暂时切到别的分支，修复完bug再切回来，而且代码也
能保留的呢？
这个时候 stash 命令就大有用处了，前提是我们的代码没有进行 commit ，哪怕你执行了add 也没关系

    * 执行： `git stash` 这样就会将暂时没有commit 的代码暂存起来，这时我们进行分支切换也就没有任何问题了
    * `git stash list`  查看暂存记录
    >当你把所有bug解决后就可以通过如下命令恢复，然后切换灰来继续做之前没做完的功能
    * `git stash apply` 将暂存区还原
    * `git stash drop stash_id(可选，删除指定记录)` 将之前最近的一次暂存记录删除，
    * `git stash pop` 还原暂存区＋删除最近一次暂存记录
    * `git stash clear` 清空所有暂存区的记录

* merge & rebase
>我们知道 merge 分支是合并的意思，我们在一个 featureA 分支开发完了一个功能，这个时候
需要合并到主分支 master 上去，我们只需要进行如下操作：

```
git checkout master
git merge/rebase featureA
```




rebase 和 merge 的区别

* rebase 跟 merge 的区别你们可以理解成有两个书架，你需要把两个书架的书整理到一起
去，第一种做法是 merge ，比较粗鲁暴力，就直接腾出一块地方把另一个书架的书全部放进
去，虽然暴力，但是这种做法你可以知道哪些书是来自另一个书架的；第二种做法就是
rebase ，他会把两个书架的书先进行比较，按照购书的时间来给他重新排序，然后重新放置
好，这样做的好处就是合并之后的书架看起来很有逻辑，但是你很难清晰的知道哪些书来自
哪个书架的。

>也就是 经**merge**合并后的分支记录并不是只有主干一条，像小河流汇入大河一样，主干分支清晰可见，而经**rebase** 合并后的分支记录只有主干一条，分支是不可见的，所有分支按时间顺序汇入主干中。   


* 总结：merge 来路可循但时间节点较乱，rebase时间节点清晰但来路不明

* 解决冲突：有conflit的时候git会智能提示，冲突的地方由 ==== 分出了上下两个部分，上部分一个叫HEAD 的字样代表是我当前所在分支的代码，下半部分是一个叫 baidu_activity 分支的代码，可以看到 HEAD 对 gradle 插件进行了升级，同时新增了一个插件，所以我们很容易判断哪些代码该保留，哪些代码该删除，我们只需要移除掉那些老旧代码，而且同时也要把那些<<< HEAD、==== 以及 >>>>>>baidu_activity 这些标记符号也一并删除，最后进行一次
commit 就ok了。
---
**2022.3.22 更新**
> 关于git commit 以及 git add 后的撤销问题

###  撤销命令：git reset

* 首先对于仓库的第一次commit提交,通过以下命令撤销

    `git update-ref -d HEAD`

* 对于大于灯与两次的提交可通过三种方式达到对 commit 、add 的不同撤销方式
    >格式: `git reset 参数  HEAD回撤次数`
   
  1. 参数：
     * --soft ：仅撤回commit操作，保留 add 和本地工作区代码
     * --mixed(默认) : 同时撤回 commit 和 add操作，保留本地工作区代码
     * --hard : 将commit 、add 以及本地工作区代码都重置，即清空暂存区和工作区

   2. HEAD回撤次数：

        * HEAD^ 回撤一次
        * HEAD~1 回撤一次
        * HEAD~2 回撤两次
        * commit id 回撤到对应id版本次commit

    3. 查询commit id 

        通过`git log`即可查看，黄色段字符极为commit id

* git status 可以查看本地区和暂存群的文件

```
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   Autogame.py
        new file:   r.ico

------------手动分割，以上为暂存区，以下为本地区未add文件-----------
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Autogame.spec
        NewAutogame.spec
        NewGame.zip
        NewGame/
        R.png
        __pycache__/
        build/

```

如果我们此时想要查看 commit 的文件，可以通过`git show commit_id`来查看哦

参考文章：<https://www.jianshu.com/p/c2ec5f06cf1a>

*** 
### 2022.7.02更新

* git fresh ：该命令用于从远程获取代码库，告诉 Git 去获取它有你没有的数据，然后你可以通过执行 git merge 来实现将更新数据合并到你的分支的操作。
* git push 主机 本地分支:远端分支 -f :实现对远端分支的强制合并
* git branch -a : 查看远端分支名称