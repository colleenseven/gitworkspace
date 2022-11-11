---
aliases: null
create_date: 2022-10-20T23:15:58 (UTC +08:00)
tags: wx/pbi/DAX函数
pagetitle: 用一个度量值返回列表？CONCATENATEX函数你应该掌握
source: https://mp.weixin.qq.com/s/c7rH7AvxeCu9gZyJOy_e7A
author: 采悟
status: 已完成
category: 泛读文章
uid: 
---

连接文本字符串经常会用到连接符&，还有个的DAX函数CONCATENATE，可以将两个字符串连接成一个字符串，这个函数本身非常简单，使用场景也有限，不过它的迭代函数CONCATENATEX，用处非常大，之前的文章中也多次用到过这个函数。  

CONCATENATEX函数迭代表的每一行，按表达式和分隔符将每一行的字符连接为一个文本字符串，语法如下：

> CONCATENATEX(
> 
>    表，                        //迭代每一行的表
> 
>    字符串表达式，     //每一行字符串的表达式
> 
>    分隔符，            //（可选）
> 
>    排序表达式， //排序依据（可选）
> 
>    排序类型    // DESC : 降序 ; ASC : 升序（可选）
> 
> ）

由于度量值的结果都只能是一个值，当<mark style="background: #FF5582A6;">需要返回多个值时，就可以利用CONCATENATEX函数将多个值连接成一个字符串输出</mark>，下面通过几个应用场景来理解这个函数的用法。

### **1\. 返回多个类别名称**

对于多选的切片器，如果想获取切片器的选项，其结果就是一个列表，这时就可以用CONCATENATEX函数将列表合并成一个字符串来返回，比如获取产品切片器的筛选情况，度量值可以这样写：

> 产品切片器 多选\=
> 
> CONCATENATEX(
> 
>    VALUES('产品表'\[产品名称\]),
> 
>    \[产品名称\],
> 
>    "、"
> 
> )

-   第1个参数VALUES('产品表'\[产品名称\])返回切片器所选的产品列表，也就是CONCATENATEX要迭代的表；
    
-   第二个参数\[产品名称\]，是返回的字符串表达式，也就是每一行的产品名称字符；
    
-   第三个参数   "、"，是连接每个产品名称的分隔符
    

上面度量值是CONCATENATEX函数最常用的写法，一般只用前三个参数，其效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMuv84Ae1sR3bYYb7cnOIhSJnX9QluBD9LxHIgd7CwY3Z2Zfzhn3wmc01iaCS5ecqTsdP0BfdBeKzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参考：[Power BI可视化设计：用文字展示切片器的筛选情况](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080905&idx=1&sn=31fb4dd94d4a23988183f463c8e85c41&chksm=8e13bbdeb96432c89c7744d82533d86fcd469e091b4153d57b7558030ea61ef95183fe6c5e47&scene=21#wechat_redirect)  

### **2\. 返回多个类别的名称和数据**

如果不仅想展示切片器所选的产品，还需要同时展示出该产品的利润，就可以这样写个度量值：

> 产品利润 =
> 
> CONCATENATEX(
> 
>     VALUES('产品表'\[产品名称\]),
> 
>     **\[产品名称\]&"："&\[利润\]**,
> 
>     UNICHAR(10)
> 
> )

这个度量值相比前一个，**主要是第2个参数有变化，每一行的字符，本身又是产品和利润数据连在一起的字符串；**第三个参数分隔符，这里用的是UNICHAR(10)，也就是换行符，来让每个字符串单独一行来显示，用卡片图展示效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM5mO8kJBGGCniaj9icJOEG5icbiaU4CbSEznkYr8IbtvuSH25PGIhD2Y7P7oKjgghAbpnic2qRLZGzMng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

### **3\. 按顺序来展示类别名称和数据**

在上面效果的基础上，如果想让这些产品，按照利润额的高低，从上往下排列展示，就需要用到CONCATENATEX函数的第4和第5参数：

> 产品利润 从高到底\=
> 
> CONCATENATEX(
> 
>     VALUES('产品表'\[产品名称\]),
> 
>     \[产品名称\]&"："&\[利润\],
> 
>     UNICHAR(10),
> 
>     **\[利润\],**
> 
>     **DESC**
> 
> )

第四参数排序依据是按利润金额来排序；第5参数DESC表示按降序排列，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM5mO8kJBGGCniaj9icJOEG5ic6RtnO82QIvBN59bMmuhzf4icgRN6ibpk69m5UyXsqmHVoD7bemyT2S6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过排序的参数，就实现了多个字符串的按顺序连接。

通过上面3个场景，把CONCATENATEX函数的每个参数的用法都做了介绍，遇到类似的需求时，就会更理解该函数的妙处。

之前介绍的动态展示表的例子，其中第一种方法，也是用CONCATENATEX函数来实现的：[Power BI如何动态展示表？送你两种方法](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074639&idx=1&sn=03b003d199f754794c0bac8af15c50e0&chksm=8e0c5258b97bdb4e0aa92667a047bca5c7705f86a6c2b4ac66e3eefc171ca95e6891a433ecff&scene=21#wechat_redirect)
