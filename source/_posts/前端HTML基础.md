---
title: 前端基础--HTML
date: 2022-02-22 22:59:53
tags: 编程语言
---
# 前端三剑客之HTML
>将前端比作人体，那么HTML就是人体的骨架

>本文主要记录自己初学前端HTML的一些基础语法及使用见解

官方解释：HTML的全称为超文本标记语言，是一种标记语言。它包括一系列标签．通过这些标签可以将网络上的文档格式统一，使分散的Internet资源连接为一个逻辑整体。HTML文本是由HTML命令组成的描述性文本，HTML命令可以说明文字，图形、动画、声音、表格、链接等。
<!--more-->
**关于前端编辑器有很多，本地比较推荐轻量化的VScode，插件种类繁多，功能强大，在线运行的话强推 `https://jsbin.com/jodevezojo/edit?html,output`**
* 基本代码框架
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body>

</body>
</html>
```
***

* 基础标签的使用
  * h1 ~ h6使用
  ```
    <h1>我是一级标题 </h1>
    <h2>我是二级标题 </h2>
    <h6>我是六级标题 </h6>
  ```
  效果：
    <h1>我是一级标题 </h1>
    <h2>我是二级标题 </h2>
    <h6>我是六级标题 </h6>

***

  * 列表标签的使用
  ```
    <ul>
        <li>无序列表</li>
        <li>列表无序</li>
    </ul>
    <ol>
        <li>有序列表</li>
        <li>列表有序</li>
    </ol>
  ```
  效果：
  <ul>
        <li>无序列表</li>
        <li>列表无序</li>
    </ul>
    <ol>
        <li>有序列表</li>
        <li>列表有序</li>
    </ol>

***

  * 图片标签的使用
  >alt属性用于图片加载失败时提示文字
  ```
    <img
        width="100"
        height="120"
        src="https://pic.qqtn.com/up/2017-9/2017090616103913310.jpg"
        alt="加载错误啦"
        />
  ```
  效果：

 <img
        width="100"
        height="120"
        src="https://pic.qqtn.com/up/2017-9/2017090616103913310.jpg"
        alt="加载错误啦"
        />

*** 

  * 超链接标签的使用
   ```
    <a href="https://pic.qqtn.com/up/2017-9/2017090616103913310.jpg">图片链接</a>
   ```
   效果：
   <a href="https://pic.qqtn.com/up/2017-9/2017090616103913310.jpg">图片链接</a>

***

   * p标签的使用
   >p标签功能相当强大，我们可以将整段文字放入其中

   ```
    <p>这是一段斜体文本,em标签可以斜体: <em> hello world </em> </p>
    <p>这是一段加粗文本，strong标签可以加粗: <strong> hello world  </strong> </p>
   ```

   效果：
   <p>这是一段斜体文本，em标签可以斜体：<em> hello world</em> </p>
   <p>这是一段加粗文本，strong标签可以加粗：<strong> hello world </strong>  </p>

***

   * 文本输入框标签input

   1. 基础款
   ```
    <input type="text" />
   ```
  效果：

<input type="text"  />

-·-

   2. 内有提示文字加强款
   ```
    <input type="text" placeholder="请输入"/>
   ```
   效果：

   <input type="text" placeholder="请输入"/>
   
   -·-

   3. 复选框：改变type属性为checkbox
   ```
   <input type="checkbox" />复选框
   ```

   效果：
   <input type="checkbox"/>

   -·-

   4. 文件按选择控件，属性file
   ```
    <input type="file" />
   ```
   效果：

   <input type="file" />
   
   >功能相当强悍

-·-

   5. 单选框控件，属性radio
   ```
    <input type="radio"/>
   ```
   效果：
   <br><input type="radio" id="radio"/> radio1 
   <input type="radio"/>radio2
   </br>
    
   * 5.1升级版本，通过加label 标签达到点击文字同样能够选中单选框的效果
   ```
    <label>
        <input type="radio" id="radio /> radio1
    </label>
   ```
   效果：

   <label>
        <input type="radio" id="radio" /> radio1
    </label>

-·-

   6. 拖动范围控件，属性range
   ```
    <input type="range"/>
   ```
   效果：
   <input type="range"/>

   -·-

   7. 提交按钮控件，属性submit
   ```
     <input type="submit"/>
   ```

  效果：
  <input type="submit"/>

---

  * 多行纯文本编辑控件
  ```
    <textarea name="story" rols=9 cows=4> this is a story  </textarea>
  ```
  效果：

<textarea name="stroy" rols=4 cows=9>this is a textarea </textarea>




    
