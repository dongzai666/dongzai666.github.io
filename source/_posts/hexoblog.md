---
title: github+hexo 个人博客搭建
date: 2022-01-30 11:14:50
tags: 环境搭建、经验
---

# Hexo静态网页博客搭建及实现多平台同步

> 该网站基于市面上流行的NodeJs框架下的Hexo，托管于github，实现了一个个人博客的基本功能，本文主要讲解在**linux**平台下搭建hexo环境的主要步骤以及在不同平台（如想同时在windows、linux下发布、管理博客内容的工作场景）同步内容的解决方案！

> 前置内容
> * linux基本命令的使用
> * Git命令行的使用及功能

<!--more-->

## 博客网站搭建--环境配置

[参考链接1](https://zhuanlan.zhihu.com/p/108094987)
> 在搭建Hexo环境前需要配置本地环境，主要有：

* Nodejs  ：需要注意其版本，建议安装至最新版本，否则会出现报错
    * 命令行安装： `sudo apt install nodejs`,ubuntu默认安装版本8.10，其他安装方法可自行百度
    * 版本查询：`Node -v`
    * 版本更新：通过安装Node工具包**n**来实现
        * 安装n `sudo npm install n -g`
        * 安装最新稳定nodejs `sudo n stable`
* npm  ：`sudo apt install npm`
* git  : `sudo apt install git`

## 博客网站搭建--实现步骤
[参考链接2](https://zhuanlan.zhihu.com/p/115153910)

1. 当前期需要环境准备好以后，配置hexo环境就相当简单了，使用命令： `sudo nmp install hexo-cli -g`
2. 然后在本地新建一个文件夹，通过`hexo init 本地文件夹路径`在指定文件夹生成文件体系，需要我们自定义的文件夹如下：
    * source/_posts 文件夹下存放.md 格式的博客文章
    * themes 文件夹下存放主题
    * 可以去github克隆喜欢的主题到该目录下，然后通过修改 _config.yaml 中 theme 字段为克隆主题生效！

3. 接下来就是将我们的网站挂载到github仓库上，这样任何人就能通过我们的网址来访问我们的网站了
    * 首先创建名为**xxx.github.io**的github仓库，以后就可以通过 xxx.github.io 的网址来访问了
    * 通过如下命令来关联本地markdown文件与远端github仓库
    ```
    npm install hexo-deployer-git --save
    ```
    * 打开配置文件_config.yml 配置git
    ```
    deploy:
    type: git
    repo: https://github.com/xxx/xxxx.github.io.git
    ```

4. 可以给自己的博客加上评论功能，这样会高逼格一点
    * 可以在畅言网站上免费注册z-blog功能，获取到**appid** 和 **appsecret**进入你的themes/对应主题,打开_config.yml，定位到 changyan ，把 enable 改为 true。
    * 然后是修改如下
    ```
    changyan:
    enable: true
    appid: 这里写上你的畅言在appid
    appkey: 这里写上你的畅言在appkey
    ```
5. 最后是通过以下命令实现本地刷新并上传到远程仓库

    * 网站修改后刷新生效命令
    ```
    hexo clean  #清除本地原缓冲文件 
    hexo g      #生成新网站，刷新  generate
    hexo s      #启动服务器 server
    ```
    * 部署网站到远端

    ```
    hexo d #deploy部署
    ```
## 博客网站搭建--部署报错
* 报错信息如下：
```
penSSL SSL_read: Connection was reset, errno 10054
FATAL {
  err: Error: Spawn failed
      at ChildProcess.<anonymous> (F:\Blog\node_modules\hexo-util\lib\spawn.js:51:21)
      at ChildProcess.emit (node:events:390:28)
      at ChildProcess.cp.emit (F:\Blog\node_modules\cross-spawn\lib\enoent.js:34:29)
      at Process.ChildProcess._handle.onexit (node:internal/child_process:290:12) {
    code: 128
  }
} Something's wrong. Maybe you can find the solution here: %s https://hexo.io/docs/troubleshooting.html
```
**在最后一部`hexo d`时出现以上的错误，不要怀疑，是GitHub的服务器出毛病了！！！多尝试几次就欧克。**


***
## 博客网站搭建--多端同步

> 解决方案，使用GitHub的分支！在博客对应的仓库中新建一个分支。一个分支用来存放Hexo生成的网站原始的文件，另一个分支用来存放生成的静态网页,通过在不同平台拉取实现资源文件同步。
* 分支master：静态网页资源
* 分支sync：网站原始文件


1. 在github网页端创建基于master的分支sync(此时sync的文件同master完全一致)，将本地生成网站原始文件转移至其他文件夹，防止待会pull时被覆盖
2. Git操作
  *  git init 初始化文件夹，生成.git文件
  *  git remote add origin https://github.com/dongzai666/dongzai666.github.io.git  链接远程仓库
  *  git pull origin sync:master 将sync分支内容拉下来，与本地建立链接，然后删除除了.git以外的所有文件

3. 将转移的网站原始文件复制回来，修改.gitignore文件，避免上传一些不需要的文件，内容如下：

  ```
  .DS_Store
  Thumbs.db
  db.json
  *.log
  node_modules/
  public/
  .deploy*/
  ```
> 如果你之前克隆过theme中的主题文件，那么应该把主题文件中的.git文件夹删掉，因为git不能嵌套上传

1. 通过
 `git push origin master:sync -f`
    **强制覆盖远端sync分支的内容**

    此时就实现了远端master分支存放生成的静态网页，sync分支用来存放网站原始文件的目的！！！

5. 之后在其他平台只需要先pull远端sync分支代码，修改完毕后再push上去即可，其他网站更新部署仍然同原来一致。