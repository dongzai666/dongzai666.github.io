---
title: python_class
date: 2022-03-17 21:08:49
tags: 编程语言
---

# Python学习之-类(calss)
> 本文主要记录下自己对python类相关知识的一些理解，平时也经常使用python来完成一些项目，不过由于没有像c/c++ 那样系统的学习，所以很多概念上存在模糊，此番重点钻研，记录所学

> python用多了就会觉得python真香，有很多现成的库可以调用，不用像c/c++ 那样造轮子啦~ 话虽如此，各有长短，没有绝对哪一门语言更好的说法，只有哪个语言更适合！

<!--more-->

## 基础概念知识
>python是面向对象的编程语言，而面向对象语言的最基本特征就是**类**和**实例**
* 理论解释
  1. 类：用于定义抽象的对象模型，它是描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。
  2. 类属性（类变量）：是该类的所有实例化对象所公用的，定义在类中且在函数体方法以外。通常不用做实例化对象。
  3. 实例属性（实例变量）：其值是当前实例化对象所特有的，所有实例化对象都有但值不一样，定义在**__init__()** 函数当中
  4. 方法：类中定义的函数。**def（）**
  5. 方法重写：如果从父类继承的方法（即函数）不能满足子类的需求，可以对其进行改写，该过程叫做方法的覆盖，也称作方法的重写。
  6. 实例化：创建一个类的具体对象的过程，类似于c语言中定义变量的过程。
  7. 实例：根据类定义的抽象模型创建出来的具体对象。
  8. 数据成员：类变量或者实例变量用于处理类及其实例对象的相关的数据。
  9. 继承：即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。

* 实例解释

    * 问题：在我们定义一个关于“人”的个人信息的类
    * 分析：<br>

        1. 类属性：所有人都共有的且相同的信息如：国籍 
        2. 实例属性：所有人都共有但不相同的信息如：姓名、性别、年龄
        3. 方法：用来打印出每个人信息的函数
        4. 实例化：用该类去定义一个具体的人
        5. 实例：用该类定义的这个具体的人就是一个实例
        6. 数据成员：初始化实例对象所需要的参数，即传入__init__()函数中的参数
        7. 继承：如果某一个人还具有其他额外的个人信息可通过继承“人”类来具有“人”类的所有方法属性，同时可进行额外扩展
        8. 方法重写：如果从基类“人”类中继承来的方法不能满足需求可对其进行改写
        > 类属性和实例属性在类外和类内的调用：<br>
        类内：1.类属性：直接使用  2.实例属性：self.实例属性名<br>
        类外：1.类属性：**类名.类属性名** 2.实例属性：**实例名.实例属性名
    * 实现

        >在Python中，类通过 class 关键字定义，类名通用习惯为首字母大写，Python3中类基本都会继承于object类，当然也可以不继承object类；两者区别不大，但没有继承于object类使用多继承时可能会出现问题。
        ```
        class Person(object):       #object是继承的基类
            address = "国家"        #类属性
    
        #类中的函数与一般函数的唯一区别是：第一个参数要加self(也可以是其他的名称，但一般统一用self)，self 代表类的实例，是通过类创建的实例！

        #__init__()函数中的name，sex，age都是数据成员

            def __init__(self,name，sex，age):
                self.name = name    #实例属性
                self.sex = sex      #实例属性
                self.age = age      #实例属性

            def print_information(self):  #该类定义的方法
                print(self.name,'性别',self.sex,'年龄',self.age)
        
        if __name__ == '__main__':
            小明 = Person('小明','男',19) 
            #实例化一个类对象，需要传入数据成员，因为当创建实例时，__init__() 方法会被自动调用为创建的实例增加实例属性。
            小明.print_information() #调用类方法
            Person.address = 'xxxx'  #改变类对象的值

        ```
* **关于`if __name__ == '__main__':`用途的解释:**<br>
    * 一个python文件通常有两种使用方法，1.是作为脚本直接执行，2. import 到其他的 python 脚本中被调用（模块重用）执行。
    * 因此 if __name__ == 'main': 的作用就是控制这两种情况执行代码的过程，在 if __name__ == 'main': 下的代码只有在第一种情况下（即文件作为脚本直接执行）才会被执行，而 import 到其他脚本中是不会被执行的。
    > 通俗来将就是在该行代码下的代码只有在当前文件作为主文件（类似与c语言中的main）时才会被执行，如果该文件作为模块被其他文件引用了，那么在其他文件中调用该文件时，这些代码时不会被执行滴！！！
    * 因为我们通常会在单独文件中写一些测试代码，这样通过该方法就可以避免作为模块时测试代码被执行的尴尬场面。。。

## 进阶知识

1. 私有方法、属性的限制：<br>

    * 通过在方法、属性前加双下划线`__`来实现，此时它们只能在类内部调用，在类外部只能通过特殊机制调用，但我们不建议这么做，毕竟这样会违背我们将其定义为私有属性的初衷！
    > 特殊机制（提一嘴）：可以通过将方法/属性写成 _类名__xx(xx为属性/方法名)来调用<br>
    如定义： __address = ‘国家’  调用：Person._Person__adderss<br>
    定义： __print_information()   调用：小明._Person__print_information()

2. Python类中的@classmethod、@staticmethod 装饰方法

    * 共同点：二者在使用时都不需要去实例化对象，可以直接通过类名来访问
    * 不同点：@classmethod 用来修饰方法。使用在实例化前与类进行交互，但不和其实例进行交互的函数方法上。<br>

    @staticmethod 用来修饰类的静态方法。使用在有些与类相关函数，但不使用该类或该类的实例。如更改环境变量、修改其他类的属性等。<br>

    两者最明显的区别，classmethod 必须使用类的对象作为第一个参数，而staticmethod则可以不传递任何参数

>一句话：@staticmethod 修饰的方法是放在类外的函数，我们为了方便将他移动到了类里面，它对类的运行无影响


   * 实例：
```
class Date(object):
   day = 0
   month = 0
   year = 0

   def __init__(self, year=0, month=0, day=0):
       self.day = day
       self.month = month
       self.year = year

   @classmethod
   def from_string(cls, date_as_string):
       year, month, day = date_as_string.split('-')
       date = cls(year, month, day)
       return date

   @staticmethod
   def is_date_valid(date_as_string):
       """
      用来校验日期的格式是否正确
       """
       year, month, day = date_as_string.split('-')
       return int(year) <= 3999 and int(month) <= 12 and int(day) <= 31

date1 = Date.from_string('2012-05-10')
print(date1.year, date1.month, date1.day)
is_date = Date.is_date_valid('2012-09-18') # 格式正确 返回True
```
>注意：@staticmethod修饰方法 is_date_valid(date_as_string)中无实例化参数self或者cls；而@classmethod修饰的方法中有from_string(cls, date_as_string) 类参数cls。

3. @property 将类方法转换为只读属性（常用）

>使用 property 的最简单的方法是将它作为装饰器来使用。这可以让你将一个类方法转变成一个类属性。

   * 示例：
  ```
        class Circle(object):
        __pi = 3.14

        def __init__(self, r):
            self.r = r

        @property
        def pi(self):
            return self.__pi

        circle1 = Circle(2)
        print(circle1.pi)
        circle1.pi=3.14159  # 出现AttributeError异常

```
>上面示例装饰了pi方法，创建实例后我们可以使用circle1.pi 自己获取方法的返回值，而且他只能读不能修改。

## 类的继承

1. 继承的实现（继承最主要用处是提高代码的重用）

    * 实现

    ```
        class Animal(object): #父类：动物类--继承基类object
            def __init__(self,name,age):
                self.name = name
                self.age = age
            def call(self):
                print(selc.name,'会叫')

        #定义子类喵喵类，继承自动物类,但多了属性性别
        class Cat(Animal):
            def __init__(self,name,sex,age):
                super(Cat,self).__init(name,age)
                self.sex = sex
            
    ```
>1.`super(子类名,self).__init__(基类数据成员，不用加self)`在派生类初始化的时候要加上，相当重要，否则，继承自 Animal的 Cat子类将没有 name和age两个属性。<br>

>2.函数super(Cat, self)将返回当前类继承的父类，即 Animal，然后调用__init__()方法，注意self参数已在super()中传入，在__init__()中将隐式传递，不能再写出self。

2. 子类方法的重构
* 类方法的调用顺序，当我们在子类中重构父类的方法后，Cat子类的实例先会在自己的类 Cat 中查找该方法，当找不到该方法时才会去父类 Animal 中查找对应的方法。<br>


* **所以对于需要重构的父类方法，我们只需要在子类中重新定义即可（函数名相同即可），然后在子类实例化时会自动覆盖！！**

* 示例：
     ```
        class Cat(Animal):
            省略

            def call(self):
                printf(self.name,'会喵喵叫')
     ```

## 多态
* 类具有继承关系，并且子类类型可以向上转型看做父类类型，如果我们从 Animal 派生出 Cat和 Dog，并都写了一个 call() 方法，如下示例：
    ```
    class Animal(object):  
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def call(self):
        print(self.name, '会叫')

    class Cat(Animal):
    def __init__(self, name, age, sex):
        super(Cat, self).__init__(name, age)
        self.sex = sex

    def call(self):
        print(self.name, '会“喵喵”叫')

    class Dog(Animal):
    def __init__(self, name, age, sex):
        super(Dog, self).__init__(name, age)
        self.sex = sex
    def call(self):
        print(self.name, '会“汪汪”叫')
    ```
我们定义一个 do 函数，接收一个变量 ‘all’,如下：
```
    def do(all):
    all.call()

    A = Animal('小黑',4)
    C = Cat('喵喵', 2, '男')
    D = Dog('旺财', 5, '女')

    for x in (A,C,D):
    do(x)
```

输出结果：
```
小黑 会叫
喵喵 会“喵喵”叫
旺财 会“汪汪”叫
```
---
* 多态解释

    >这种行为称为多态。也就是说，方法调用将作用在 all 的实际类型上。C 是 Cat 类型，它实际上拥有自己的 call() 方法以及从 Animal 继承的 call 方法，但调用 C .call() 总是先查找它自身的定义，如果没有定义，则顺着继承链向上查找，直到在某个父类中找到为止。

    >传递给函数 do(all) 的参数 all 不一定是 Animal 或 Animal 的子类型。任何数据类型的实例都可以，只要它有一个 call() 的方法即可。其他类不继承于 Animal，具备 call 方法也可以使用 do 函数。这就是动态语言，动态语言调用实例方法，不检查类型，只要方法存在，参数正确，就可以调用。