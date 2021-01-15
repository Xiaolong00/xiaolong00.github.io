---
title: 记一次mysql的教训
date: 2021-01-09 08:17:39
tags: [编程, 过去]
category:
    - 100 学习类
    - 110 编程
    - 113 数据库
---

## 新知识
### 字符串的字典序  
字典序（dictionary order），又称 字母序（alphabetical order），原意是表示英文单词在字典中的先后顺序，在计算机领域中扩展成两个任意字符串的大小关系。   
在Java语言中，**System.out.println("ah1x".compareTo("ahb"));**会输出 -49−49，这个数是两个字符串第一个不一样的位置的两个字符的 ASCII 值之差，如果小于零则说明第一个字符串小于第二个字符串。  
除此之外，大多数语言也都有对应的字符串比较方法，而背后的核心都是字符串的字典序。理解并掌握这个重要的概念，对今后计算机专业课程的学习和程序开发都至关重要。  


## 场景复现
问题：我有一个名为hexcodetable的MySQL表，只有一个名为VARCHAR（100）的名为hexcode的列。该表包含所有十六进制颜色代码。这些行填充为六个字符的十六进制数字，后跟＃。例如，＃25F412。我们如何对从最黑到最白的所有行进行排序，使得第一行为＃000000，第二行为＃000001，最后一行为#FFFFFF？请注意，我不一定要进行数字排序。    
答案：按十六进制值进行数字排序。  
```
Select hexcode from hexcodetable order by Conv(substring(hexcode,2,6),16,10)
```
### 详解
- MySQL conv()函数  
CONV(N,from_base,to_base)  
所述CONV()函数的目的是在基数之间进行转换。该函数返回值N从from_base到to_base转换的字符串。最小基数值是2，最大值为36。如果任一参数为NULL，则该函数返回NULL。考虑下面的例子，其中数字 5 将从基数16转为基数2   
  ```
      mysql> SELECT CONV(5,16,2);
    +---------------------------------------------------------+
    | CONV(5,16,2)                                            |
    +---------------------------------------------------------+
    | 101                                                     |
    +---------------------------------------------------------+
    1 row in set (0.00 sec)

  ```
### 延伸bug
这条sql里面有个坑就是，有时按照某个字段的大小排序（或是比大小）发现排序有点错乱。后来才发现，是我们想当然地把对字符串字段当成数字并按照其大小排序（或是比大小），结果肯定不会是你想要的结果。  
这时候需要把字符串转成数字再排序，最简单的办法就是在字段后面加上+0。   
- 排序：  
例：  
方法一：ORDER BY '123'+0;（首推）  
方法二：ORDER BY CAST('123' AS SIGNED);  
方法三：ORDER BY CONVERT('123',SIGNED);  
















































