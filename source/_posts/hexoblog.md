---
title: github+hexo 个人博客搭建
date: 2022-01-30 11:14:50
tags: 环境搭建、经验
---
# 博客搭建要点及步骤
> 俺认为新建一个博客网站还是挺容易的，接下来总结下主要步骤要点
<!--more-->
1. 安装**nodejs** ，利用里面的**hexo**框架可以搭建博客
    * 通过hexo初始化我们的博客仓库，也就是生成一个文件夹
    * source/_posts 文件夹下存放.md 格式的博客文章
    * themes 文件夹下存放主题
    > 可以去github克隆喜欢的主题到该目录下，然后通过修改 _config.yaml 中 theme 字段为克隆主题生效！

2. 此时我们的网站只能在本地运行登录，接下俩需要挂载到github仓库中方可全网访问
    * 网站修改后刷新生效命令
    ```
    hexo clean  
    hexo g      #生成新网站，刷新  generate
    hexo s      #启动服务器 server
    ```
3. 可以给自己的博客加上评论功能，这样会高逼格一点
    * 可以在畅言网站上免费注册z-blog功能，获取到**appid** 和 **appsecret**进入你的themes/对应主题,打开_config.yml，定位到 changyan ，把 enable 改为 true。
    * 然后是修改如下
    ```
    changyan:
    enable: true
    appid: 这里写上你的畅言在appid
    appkey: 这里写上你的畅言在appkey
    ```
    然后刷新配置三件套就可以了！
    ***
4. 接下来就是将我们的网站挂载到github仓库上，这样任何人就能通过我们的网址来访问我们的网站了
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
    * 最后一步，将网站部署到github上去
    ```
    hexo d 
    ```
## 部署时报错的坑
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