---
layout: post
title: Python入门
description: 一起学Python系列（一）
category: blog
date: 2020-01-07 13:50:39
---

## 翻到以前阅读过的博客的一段话  
关于学习新知识我有一点心得体会想与你分享。我在学习新知识的时候会遵循一个5-20-2法则，用5分钟的时间了解这个新知识的特点、应用场景、要解决的问题；用20分钟理解它的主要设计原理、核心思想和思路；再花2个小时看关键的设计细节，尝试使用或者做一个demo。   
如果5分钟不能搞懂它要解决的问题，我就会放弃；20分钟没有理解它的设计思路，我也会放弃；2个小时还上不了手，我也会放一放。你相信我，一种真正有价值的好技术，你这次放弃了，它过一阵子还会换一种方式继续出现在你面前。这个时候，你再尝试用5-20-2法则去学习它，也许就会能理解了。我学Hadoop实际上就是经历了好几次这样的过程，才终于入门。而有些技术，当时我放弃了，它们再也没有出现在我面前，后来它们被历史淘汰了，我也没有浪费自己的时间。   
还有的时候，你学一样新技术却苦苦不能入门，可能仅仅就是因为你看的文章、书籍本身写的糟糕，或者作者写法跟你的思维方式不对路而已，并不代表这个技术有多难，更不代表你的能力有问题，如果换个方式、换个时间、换篇文章重新再看，可能就豁然开朗了。  

## Python基础

### 环境搭建
搭建python3.7

### IDE安装
安装PyCharm

### 运行您的第一个Python程序
1. 新建 hello.py 文件，输入：  
print("Hello, Python")  
2. 脚本文件添加可执行权限  
chmod +x test.py  
3. 运行  
./test.py  
4. 输出结果  
Hello, Python!  

### Python 标识符
在 Python 里，标识符由字母、数字、下划线组成，但不能以数字开头。  
以下划线开头的标识符是有特殊意义的。以单下划线开头 _foo 的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用 from xxx import * 而导入。  
以双下划线开头的 __foo 代表类的私有成员，以双下划线开头和结尾的 __foo__ 代表 Python 里特殊方法专用的标识，如 __init__() 代表类的构造函数。  
Python 可以同一行显示多条语句，方法是用分号 ; 分开  

### 行和缩进
Python 的代码块不使用大括号 {} 来控制类，函数以及其他逻辑判断，而是用缩进来写模块。缩进的空白数量是可变的，但是所有代码块语句必须包含相同的缩进空白数量，这个必须严格执行。  

### 多行语句
Python语句中一般以新行作为语句的结束符。但是我们可以使用斜杠（ \）将一行的语句分为多行显示，语句中包含 [], {} 或 () 括号就不需要使用多行连接符。  

### Python 引号
Python 可以使用引号( ' )、双引号( " )、三引号( ''' 或 """ ) 来表示字符串，引号的开始与结束必须是相同类型的。
其中三引号可以由多行组成，编写多行文本的快捷语法，常用于文档字符串。   

### Python注释
python中单行注释采用 # 开头。python 中多行注释使用三个单引号(''')或三个双引号(""")。

### import 与 from...import
在 python 用 import 或者 from...import 来导入相应的模块。  
将整个模块(somemodule)导入，格式为： import somemodule  
从某个模块中导入某个函数,格式为： from somemodule import somefunctio  
从某个模块中导入多个函数,格式为： from somemodule import firstfunc, secondfunc, thirdfunc  
将某个模块中的全部函数导入，格式为： from somemodule import *  

### 标准数据类型
Python有六个标准的数据类型：    
- Numbers（数字）
- String（字符串） 
- List（列表）
- Tuple（元组）
- Set（集合）
- Dictionary（字典）  
不可变数据（3 个）：Number（数字）、String（字符串）、Tuple（元组）;   
可变数据（3 个）：List（列表）、Dictionary（字典）、Set（集合）。  

#### Python数字
支持 int、float、bool、complex（复数），内置的 type() 函数可以用来查询变量所指的对象类型。    
- isinstance 和 type 的区别在于：  
type()不会认为子类是一种父类类型。  
isinstance()会认为子类是一种父类类型。  
当你指定一个值时，Number 对象就会被创建：  
您也可以使用del语句删除一些对象引用。  

#### tring（字符串）
字符串或串(String)是由数字、字母、下划线组成的一串字符。    
python的字串列表有2种取值顺序:  
从左到右索引默认0开始的，最大范围是字符串长度少1   
从右到左索引默认-1开始的，最大范围是字符串开头   
从字符串中获取一段子字符串的话，含头不含尾。  

#### List（列表）
列表用 [ ] 标识，是 python 最通用的复合数据类型。  
加号 + 是列表连接运算符，星号 * 是重复操作。  

#### Tuple（元组）
元组（tuple）与列表类似，不同之处在于元组的元素不能修改。元组写在小括号 () 里，元素之间用逗号隔开。   

#### Set（集合）
集合（set）是由一个或数个形态各异的大小整体组成的，构成集合的事物或对象称作元素或是成员。  
可以使用大括号 { } 或者 set() 函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。   

#### Dictionary（字典）
列表是有序的对象集合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。  
字典是一种映射类型，字典用 { } 标识，它是一个无序的 键(key) : 值(value) 的集合。  
键(key)必须使用不可变类型。  
在同一个字典中，键(key)必须是唯一的。  











## Jupyter 使用

### 安装jupyter
pip3 install jupyter

### 启动jupyter
启动jupyter  
jupyter notebook  
指定英文开启  
LANGUAGE="" LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 jupyter notebook  

### jupyter基本功能
运行python代码  
运行代码文件保存到磁盘  
markdown格式编写注释  
















































