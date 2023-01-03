---
create_date: 2022-12-06T23:50:08 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何在Power BI折线图中添加平均线？
source: https://mp.weixin.qq.com/s/_CcFiQ7l-RcNzDmbjr7Skg
author: 采悟
status: 已完成
category: 精读文章
notes: False
ZK: Origin
uid: 
---

DAX:: IF,SELECTEDVALUE ,AVERAGEX ,ALL ,CALCULATE, TREATAS  ,VALUES 

这是来自于星友的一个问题，如何在折线图中增加一条平均值的折线？为了说明这个问题，以PowerBI星球的案例数据为例，这里三个产品类别12个月的销售收入折线图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOa6zmfQRCLeWwgIR5m4s4rDseMCDmKQ0blZW39LyVvUibheNdsiadrlicUH9e5CXTfWVtnasPxoKicxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果使用自带的添加平均值线的功能，它展现的是一条直线。

上图中的平均值，展示的是全年每个月份每个产品类别整体的均值，和每个月份无关，所以是一条各月份相等的直线。如果想添加一条按月计算的平均值折线，应该怎么做呢？  

对于多系列的折线图，如果每一条折线是一个独立的度量值，这种相对简单，再写一个平均值的度量值放到折线图中即可。

<mark style="background: #ADCCFFA6;">多系列折线图更常规更简单的做法是只有一个度量值，在图例中放入字段</mark>，上图就是这样做的，图例中是产品类别字段，每条折线表示一个类别，如果想添加一条折线，就需要在图例中添加一个类别。

整体思路是<mark style="background: #ADCCFFA6;">先构造带平均值的图例字段，并用DAX来实现每月均值的计算</mark>，下面就以这种做法来看看实现步骤。

**1\. 创建辅助表**

先建立一个辅助表，在产品类别中添加一个“平均值”的类别，方式如下：  

关于创建辅助表的更多方式请参考：[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)

**2\. 建立度量值**

辅助表中有了"平均值"，但是它并不能自动计算出平均的结果，需要使用DAX来让它产生平均的结果：

> 带均值的收入 =
> 
> IF(
> 
>     SELECTEDVALUE('辅助表'\[产品类别\])="平均值",
> 
>     AVERAGEX(ALL('产品表'\[产品类别\]),\[收入\]),
> 
>     CALCULATE(\[收入\],TREATAS(VALUES('辅助表'\[产品类别\]),'产品表'\[产品类别\]))
> 
> )

这个度量值逻辑是<mark style="background: #ADCCFFA6;">判断上下文是否为“平均值”</mark>，如果是，就返回所有产品类别的均值，否则正常返回每个类别的收入。

因为辅助表并没有与其他表建立关系，所以这里用了TREATAS来将辅助表的产品类别与产品表的产品类别联系起来，才能正确计算出每个类别的数据。  

**3\. 绘制折线图**

这里将辅助表中的产品类别作为图例，上面写的度量值作为折线图的值，就在折线图中多了一条平均值线（绿色）。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOa6zmfQRCLeWwgIR5m4s4r5QIhYKawZWj6M9QMm4EeJZe7QxC0jKauQJjGib6RV7bg1sBWuicGsNyQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就很简单的实现了在折线图中添加一条平均值折线的需求，关键是熟悉折线图的原理，相应的去进行构造数据结构和度量值。
