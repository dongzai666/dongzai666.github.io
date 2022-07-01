---
title: CodeExperience
date: 2022-03-17 08:11:57
tags: 编程经验
---

# Coding经验贴

> 本文主要记录一些coding过程中积累的零散小经验，实用性较强，同时也是为了防止遗忘，日积月累就会有质的提高

> 读起来可能会比较没有规律性，哈哈哈~

1. python之命令行运行代码文件 <br>
    在终端通过 `python 代码文件名.py` 运行<br>
  可以在python虚拟环境中运行，这样可以有效防止版本冲突！
<!--more-->

2. 在python虚拟环境下跑代码**用过的都说好** 用啥环境就装啥，完全不用担心把主环境搞坏了！

3. 在python函数内试图改变全局变量的值会报错：
```
 local variable 'xxx' referenced before assignment
```
  * 解决办法：只需要在该函数内声明该变量为global，再行修改
    `global xxx`<br>
    `xxx = x`

4. 在安装一些模块的时候如果配置环境过程比较复杂，而直接`pip install 模块`行不通的时候，可以通过下载对应的 **.whl**文件通过`pip install 文件路径\xxx.whl`来安装快捷简单，但前提是有对应的.whl文件
> 我在安装PyHook3的时候就遇到了此类问题，网上一堆教程配置繁琐且未成功，在github上找到对应的.whl即完成了安装，所有还是待好好利用github呀！

5. 如果运行某些程序代码时遇到提示缺少对应动态链接库xxx.dll情况，可直接去网上搜寻到对应文件，放置到对应位置即可
6. 今天Get到了一个Vscode快捷键，相当nice ：`alt + shift` 可以实现单列复制效果，如果不理解，可以自己上手试试就晓得了

* 基础语法，pygame，tkinter，mysqlite


1、myfont = pygame.font.Font(None,60)

     #  返回一个字体对象

     #  参数一：

          取None表示使用系统默认字体，也可以是指定的具体名字

     #  参数二：

          字体的大小

2、textImage = my_font.render(text, antialias, color)

    #  在内存中绘制文本图片，并返回一个Surface对象

    #  参数一：

        text： str, 文本内容

        antialias： bool，是否将文本的锯齿形边缘变得光滑

        color：（R,G,B),  文字颜色

3、screen.blit(textImage, (10, 100))

    # 在坐标（10， 100）处展示textImage

* 关于pymssql模块安装失败问题，可以通过第三方 .whl文件来解决，但是呢，俺是在python虚拟环境下进行的，网上都说是在 python的Scripts文件夹下进行安装，而我按捺住稍微优点慌的心情，毕竟环境问题可不是闹的，但俺一想那俺是不是可以在虚拟环境下指定 .whl文件的路径就可以了呢，结果 ---- 成功啦！！！

  ```
  pip install D:\PyMssql\pymssql-2.1.5-cp36-cp36m-win_amd64.whl 
  ```

* 关于文本处理

>在生活中我们通常会遇到文本或数据不符合自己需求的情况，此时需要进行处理，多脏数据进行清理，以期达到我们的需求，此时通常会用到正则表达式


  * * ^表示从每一段开头开始匹配  
    * $表示匹配到每行行末
    * [0-9]表示数字  
    * {重复出现的次数}
    * [.]表示符号'.'
    * \n 回车
    * .*? 可以表示任意字符


  1. 开头的有序序号，如` 1. 2. ~ 100. `等<br>Code `^[0-9]{1}[.]`
    通过改变重复次数来消除所有序号

  2. 消除如`v. xxxxx`等<br>Code`v[.].*?$`

  