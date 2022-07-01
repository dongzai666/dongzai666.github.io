---
title: Virtual_environment
date: 2022-03-16 01:36:58
tags: 环境搭建、经验
---

# 创建pyhton虚拟环境

> 使用场景：对于python程序进行打包的时候，由于我们电脑安装了Anaconda或者过多的其他包导致打包生成的exe文件相当大，同时运行相应时间也较长！

> 解决方案：在电脑上新建一python虚拟环境，专用于打包程序<br>虚拟环境可以理解为是Python解释器的一个副本，在这个环境你可以安装私有包，而且不会影响系统中安装的全局Python解释器。虚拟环境非常有用，可以在系统的Python解释器中避免包的混乱和版本的冲突。【重要是不同虚拟环境可以搭建不同的python版本，创建时候选择】

<!--more-->
## 详细 步骤
> 首先本地要有python环境，可以通过 可以在电脑左下角搜索【编辑系统环境变量】——【用户变量】——【PATH】中找到 

1. 创建虚拟环境包安装

```
pip install virtualenv
pip install virtualenvwrapper-win 
```

2. 创建虚拟环境

```
mkvirtualenv -p="python环境所在路径\python.exe" 虚拟环境名称
```

**此时我们虚拟环境已经创建好了，就是我们的对应环境名称**

3. 进入虚拟环境

    `workon 虚拟环境名 `

```
G:\项目测试文件夹\NewAutogame>workon pynew
(pynew) G:\项目测试文件夹\NewAutogame>
```
>可以看到在当前目录前面有括号包围起来的虚拟环境名称，说明此时我们已成功切换


通过 `pip list` 可以查看当前虚拟环境已安装的依赖

```
(pynew) G:\项目测试文件夹\NewAutogame>pip list
Package    Version
---------- -------
pip        21.3.1
setuptools 59.6.0
wheel      0.37.1
```

4. 然后运行代码，查看缺少哪些依赖，对应安装即可

   运行代码 `python 代码名.py`<br>安装依赖 `pip install 依赖名`


**同时pyinstaller模块必须重新安装，文件才会缩小**

5. 退出虚拟环境

    通过命令 `deactivate`  退出虚拟环境

    ```
    (pynew) G:\项目测试文件夹\NewAutogame>deactivate

    G:\项目测试文件夹\NewAutogame>
    ```
6. 删除虚拟环境<br>
    要删除虚拟环境，直接删除虚拟环境所在的目录就可以了，注意不要将其它的环境给删了
    >本人虚拟环境在`C:\Users\HP\Envs`下
---
## PyInstaller模块的使用

> PyInstaller是一个能将Python程序转换成单个可执行文件的程序，操作系统支持Windows, Linux, Mac OS X, Solaris和AIX。 并且很多包都支持开箱即用，不依赖环境。

* 代码<br>
`pyinstaller -F -w -i ./xx.ico xxx.py`
* 参数
```
    -i 给应用程序添加图标
    -F 指定打包后只生成一个exe格式的文件
    -D –onedir 创建一个目录，包含exe文件，但会依赖很多文件（默认项）
    -c –console, –nowindowed 使用控制台，无界面(默认)
    -w –windowed, –noconsole 使用窗口，无控制台
    -p 添加搜索路径
```
>图标图片是 .ico 格式，可通过该网站转换，[友情链接](https://png2icojs.com/zh/#:~:text=ICO%E6%A0%BC%E5%BC%8F%E6%98%AFWi,6%2C32x32%E3%80%82)
<br>pyinstaller 详细学习可看此处 <a href="https://zhuanlan.zhihu.com/p/75694259">《py打包实战指南》</a>

---
## 依赖安装、卸载及外部源加速问题

1. 依赖安装

    `pip install 依赖名`
>最常用此方法，掌握此即可

2. 依赖卸载

    `pip uninstall 依赖名`

3. pip 版本升级

    `python -m pip install --upgrade pip==9.0.3`

> 经常会出现PIP版本过低而无法安装依赖问题，只需升级pip版本即可！

4. 外部源使用

>目的：解决依赖安装速度慢及安装失败问题

* 国内常用源列表
    * 清华大学 https://pypi.tuna.tsinghua.edu.cn/simple
    * 中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple
    * 阿里云 http://mirrors.aliyun.com/pypi/simple
    * 中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple
    * 豆瓣 (douban) http://pypi.douban.com/simple

>注意:关于--trusted-host（即host域名）部分，就取index-url中http(s):// 到第一个/之间的部分，请使用者自行对应提取


* pip两种源的方式使用
    * 安装时零时指定
 `pip3 install sweetest  -i https://pypi.tuna.tsinghua.edu.cn/simple`
    * 如果提示 host 不被信任可以加上参数 --trusted-host
    `pip3 install sweetest  -i https://pypi.tuna.tsinghua.edu.cn/simple --trusted-host  pypi.tuna.tsinghua.edu.cn`