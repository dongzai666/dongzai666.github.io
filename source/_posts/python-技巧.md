---
title: python-技巧
date: 2022-04-28 09:39:27
tags: 编程经验
---

>本文主要记载一些Python编程过程中的代码优化技巧，让代码跟简洁优美同时执行效率更高,一下代码均经过实敲检验！<br>

>声明：本文是参考其他博主的文章作以总结并加入自己的一些内容

## 话不多说，Let`s GO
---
**python中input()输入得到的数据类型都为str，也就是对数字进行判断的时候要进行转换--int(number)**
1. 处理用户的多个输入
* Bad Code
    <p>
    n1 = input("please input a number: ")<br>
    n1 = input("please input a number: ")<br>
    n1 = input("please input a number: ")
</p>
<!--more-->
* Good Code
    >输入数字以空格分隔，或者在.split()中指定分隔符也可
    <p>
    n1,n2,n3 = input("please input three number:").split()
    </p>

2. 处理多个条件语句

    >对于多个and语句可以用all()代替、多个or语句可以用any()代替

* Bad Code
    ``` 
    name = "apd"
    age = 20
    school = "NEU" 
    if name == "apd" and age == 20 and school == "NEU": 
        print("yes") 
    if name == "apd" or age == 20 or school == "NEU": 
        print("no")
    ```
* Good Code

    ```
    conditions= [ 
    name == "apd", 
    age == 20, 
    school == "NEU" 
    ] 
    if all(conditions): 
        print("yes") 
    if any(conditions): 
        print("no")
    ```

1. 交换变量的值，在python中无需定义中间变量temp来进行值的交换，只需要按如下操作即可

* Good Code

    <p>
    a = 100<br>
    b = 200<br>
    a,b = b,a
    </p>

4. 对字符进行反转

* Good Code
    `string[::-1]`即可，即需要反转字符串+[::-1]

* 拓展：判断字符串是否为回文串

    `string.find(string[::-1]) == 0` True为存在，False不存在

5. 使用*args传递多个参数**目测比较有用！**
* Bad Code
    <p>
    def sum_of_squares(n1,n2):<br>
        return n1^2+n2^2
    </p>

* Good Code

    <p>
    def sum_of_squares(*args):<br>
        return sum([item**2 for item in args])
    </p>
6. **列表生成式（list comprehensions）**
    **功能比较强大，具体使用时可深入学习**
    >列表生成式结构`[包含xx的表达式 for xx in yy if sss ]`<br>
    即通过遍历yy中满足sss条件的值xx，执行包含xx的表达式来生成新的列表

### 简单演示
<p>
需求：字符串s1 ='ABC'，字符串 s2 = '123'，要求：生成序列 A1 A2 A3 C1 C2 C3
    </p>

* Bad Code
    ```
    for i in s1: 
        for j in s2: 
            if i != 'B': 
                lst.append(i+j)
    ```

* Good Code

    <p>
    lst = [i+j for i in s1 for j in s2 if i!='B']
    </p>
---
## List专区
1. 删除列表中的重复元素

    >不用去便利整个列表，可以通过set()来删除重复元素<br>
* Good Code

    <p>
    lst = [1,2,3,3,5,7,8,7,8]
    print(lst)
    new_lst = list(set(lst))
    print(new_lst)
    </p>

2. 找到list中重复最多的元素
   >使用max(list,key=list.count)来找到list中重复次数最多的元素
* Good Code
    <p>
    lst = [1,2,4,5,3,4,4,5,6,7,4]<br>
    most_number_value = max(lst,key=lst.count)<br>
    </p>

3. 拼接list中的元素
   >of course你可以指定拼接符号,通过join()函数来实现 `"拼接符号".join(拼接列表)`

* Code

    <p>
    lst = ['a','p','d']<br>
    new_lst = "-".join(lst)
    </p>

4. 使用两个list生成一个字典
    >通过zip功能来实现

* Code
    <p>
    keys = ['a','b','c']<br>
    values = [1,2,3]<br>
    dct = dict(zip(keys,values))
    </p>

5. 在循环中获得list值的下标，优雅简洁写法

* Code

    >idx是下标，item是对应值
    ```
    lst = ["blue", "lightblue", "pink", "orange", "red"] 
    for idx, item in enumerate(lst): 
        print(idx, item)
    ```

---
## Dict专区
1. 合并两个字典

* Code
    <P>
    d1 = {"v1": 22, "v2": 33}<br>
    d2 = {"v2": 44, "v3": 55}<br>
    d3 = {**d1, **d2}<br>
    print(d3)   
    </P>

2. 按照字典的value值进行排序，具体其他用法可自行百度

* Code
    <p>
    d = {<br>
    "v1": 80,<br>
    "v2": 20,<br>
    "v3": 40,<br>
    "v4": 20,<br>
    "v5": 10,<br>
    }<br>
    sorted_d = dict(sorted(d.items(), key=lambda item: item[1]))<br>
    print(sorted_d) 
    </p>

