---
ZK: Origin
notes: True
aliases: null
create_date: 2022-03-31T11:56:25 (UTC +08:00)
tags: wx/pbi/DAX函数
pagetitle: 一文掌握Power BI中的IN运算符
source: https://mp.weixin.qq.com/s/APHjc9T-EU3G1axe9BslIg
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

DAX:: CALCULATE,IN,NOT,VALUES,CALCULATETABLE, SAMEPERIODLASTYEAR, INTERSECT,IF, SELECTEDVALUE,ISFILTERED

本文来学习一下DAX中经常用到的IN，它并不是一个函数，而是一个<mark style="background: #FF5582A6;">逻辑运算符，用于检查表达式是否属于值列表</mark>，IN非常的好用，下面根据几个常见的场景来看一下它的用法。  

**<mark style="background: #FF5582A6;">IN的普通用法</mark>**

以PowerBI星球常用的案例模型为例，假如要计算“U盘”的销售额，度量值可以这样写：  

销售额 U盘= 

CALCULATE(

    \[销售额\],

    '产品表'\[产品名称\]="U盘"

)

其实还可以用IN来表达，写法如下：  

销售额 U盘 = 

CALCULATE(

    \[销售额\],

    '产品表'\[产品名称\] **IN { "U盘" }** 

)

上面两个度量值返回同样的结果。

**因为IN的<mark style="background: #FF5582A6;">后面必须是一个表，对于某个值，可以用{ }括起来，将值强制构造为表</mark>。**

通过上面的例子，看起来IN 也没有什么特别之处，但是如果你要计算多个产品，IN的优势就会很明显。

比如需要计算U盘、耳机和硬盘这三个产品的销售额：

普通的写法是这样的：

销售额 U盘耳机硬盘=

CALCULATE(

    \[销售额\],

    '产品表'\[产品名称\]="U盘" ||

    '产品表'\[产品名称\]="耳机" ||

    '产品表'\[产品名称\]="硬盘"

)

如果用IN来表达：  

销售额 U盘耳机硬盘= 

CALCULATE(

     \[销售额\],

    '产品表'\[产品名称\] **IN { "U盘", "耳机" ,"硬盘" }**

)

是不是更简洁呢？  

**<mark style="background: #FF5582A6;">IN与NOT结合</mark>**

IN还可以与NOT一起使用，NOT表示否定，也是DAX中的运算符，<mark style="background: #FF5582A6;">NOT IN用来表示不在这个列表内的数据集合</mark>。

比如计算除U盘、耳机和硬盘之外的，其他产品的销售额，

销售额 除U盘耳机硬盘 =

CALCULATE(

    \[销售额\], 

    **NOT '产品表'\[产品名称\] IN { "U盘", "耳机" ,"硬盘" }**

)

这样就可以把不在这个列表内的其他产品的销售额计算出来了。

**<mark style="background: #FF5582A6;">IN用于多列</mark>**  

IN不仅用于一列，还可以用于多列。

比如要计算<mark style="background: #FF5582A6;">销往南京的U盘销售额</mark>，正常是这么写：

销售额 U盘南京 = 

CALCULATE(

    \[销售额\],

    '产品表'\[产品名称\]="U盘",'客户表'\[客户城市\]="南京市"

)

用IN 的写法如下：  

销售额 U盘南京 = 

CALCULATE(

    \[销售额\],

    **('订单表'\[产品名称\],'订单表'\[客户城市\])** 

        **IN { ("U盘","南京市") }**

)

只有<mark style="background: #FF5582A6;">一列时，{ }中可以直接输入文本，但**对于两列，同一行的两列需要用括号（）括起来，每个括号代表一行。</mark>**

再看个例子，计算销往南京的U盘销售额以及销往天津的耳机销售额合计：  

销售额 U盘南京+耳机天津= 

CALCULATE(

    \[销售额\],

    ('订单表'\[产品名称\],'订单表'\[客户城市\]) 

        **IN { ("U盘","南京市") , ("耳机","天津市") }**

)

这个例子中，IN 后面的表就是两行两列的表。  

**用<mark style="background: #FF5582A6;">IN检索虚拟表</mark>**

关于IN，除了检索用{ }构造的值列表，其实<mark style="background: #FF5582A6;">更多的场景是在度量值中，直接用于检索虚拟表</mark>，比如之前分享的动态返回表的案例:

[Power BI如何动态展示表？送你两种方法](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074639&idx=1&sn=03b003d199f754794c0bac8af15c50e0&chksm=8e0c5258b97bdb4e0aa92667a047bca5c7705f86a6c2b4ac66e3eefc171ca95e6891a433ecff&scene=21#wechat_redirect)  

其中有这个度量值：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPoT4k4an0MEQe427woeQyenllTwM3nZ6kBqptvEUBlp5ibosAaTjgWicrcIH8QTlsEAIwtDPO0tDAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这段表达式的最后一句，就是<mark style="background: #FF5582A6;">检查当前用户是否在虚拟的表中，因为VAR 定义的customers\_same本来就是一个表，所以可以直接用在IN后面，并不需要加{ }</mark>。

关于用IN来检索虚拟表也可以参考这篇文章中度量值的写法：

[PowerBI切片器，原来还可以这样交互？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074281&idx=1&sn=ea825a10f8bb56815772997dcccfff08&chksm=8e0c5dfeb97bd4e8b6bf810457b5c579cf6633545260ce2097d21bc48e187bd88f49f3c528bf&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPCJlp1D6Kibt9mGDlkENsicy8r51JkUBAic6wR3CwNPLdAjcba9zMjZSibLPMdY3tOVsDbjwoorJx6KA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

需要注意的是，如果**<mark style="background: #FF5582A6;">检查的值只有一列，则IN后面跟的虚拟表也必须只有一列</mark>**，前后必须对应，否则会报错的。

通过以上几个应用场景，你是不是完全清楚了IN 的用法呢？
