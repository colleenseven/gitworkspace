---
create_date: 2022-10-14T22:41:41 (UTC +08:00)
tags: DAX函数
pagetitle: 认识Power BI中的财务函数
source: https://mp.weixin.qq.com/s/-PkaudojWtrQX4g3PiTwNw
author: 采悟
status: 已完成 
category: 浏览文章
uid: 
---

[前面文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484082457&idx=1&sn=31519e6ea0656cf8bcccd9c86aa2172f&chksm=8e13bdceb96434d87ea55b9c93fa23970be977fa081257cf932b218734e6e821262490b072ee&scene=21#wechat_redirect)中介绍了收益率相关的计算，其实DAX中还有一类函数，专门用于这种计算，除了<mark style="background: #FF5582A6;">收益率</mark>，还有<mark style="background: #FF5582A6;">折旧、现值/终值、投资回报期</mark>等财务场景的计算，这就是<mark style="background: #FFB86CA6;">DAX财务函数</mark>。

财务函数是将一些常用的、规律性的财务计算逻辑，封装成函数，以便帮助用户更快捷实现特定的计算。

目前已经有51个财务函数，关于这些函数的作用和语法可参考官方文档：

https://learn.microsoft.com/zh-cn/dax/financial-functions-dax

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPpxUialroCHdtfqZAKESdxC7LT6KLA6Iiad4U8b6gkjSB3mSCthiaHYhQyib1r4rDvKVwKtLPJicq5vVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里挑选几个常用的函数带你了解一下财务函数的基本用法。

**PV** 

根据<mark style="background: #FF5582A6;">固定利率计算现金流的现值</mark>

假如每月还<mark style="background: #FFB86CA6;">房贷</mark>5000元，年利率5%，20年还清，则现值（也就是初始贷款额）可以这样计算：

> 贷款额(20年月供5000年息5%) = PV( 0.05/12 , 20\*12 , -5000)

其中0.05/12是将年利率折算为月利率，20\*12是总还款月数，这里要确保利率和还款频次是对应的，结果如下：  

**FV**

根据<mark style="background: #FF5582A6;">固定利率计算现金流的终值</mark>

FV与PV正好相反，如果你每月存5000，年利率5%，你想知道存够20年以后会变成多少钱，就可以用这个函数：  

> 月存五千20年后有多少钱 \= FV(0.05/12,20\*12,-5000)

按这个利率每月存5000,20年后你能得到大约205万。

## **PDURATION**

返回<mark style="background: #FF5582A6;">投资达到指定值所需的期数</mark>

比如年收益率10%，投入5万元，多少年后可以得到10万，也就是投资翻倍需要的年数，就可以用这个函数来计算。  

> 收益率10%几年可翻倍 =PDURATION(0.10,50000,100000)

收益率为10%时，大约7.2年投资可翻番。

**RRI**

返回<mark style="background: #FF5582A6;">投资的每期收益率</mark>

通过这个函数，已知现值、终值和期数，就可以计算出每期的收益率。  

比如投资100元，5年后获得200元，也就是5年投资收益翻一倍，其年化收益率是多少呢？  

可以用RRI函数这样写度量值：

> 5年翻倍的年化收益率 \= RRI( 5 , 100 , 200 )

收益率达到14.87%才能在5年内投资翻倍。

这个函还可以运用到[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484082457&idx=1&sn=31519e6ea0656cf8bcccd9c86aa2172f&chksm=8e13bdceb96434d87ea55b9c93fa23970be977fa081257cf932b218734e6e821262490b072ee&scene=21#wechat_redirect)中关于年化收益率的计算，之前是用了POWER函数，其实用RRI，它也可以计算年化收益率：  

**XIRR**

返回<mark style="background: #FF5582A6;">不一定具有周期性的现金流时间表的内含收益率</mark>

上面RRI计算每期收益率，是在非常规律的周期性现金流的基础上的，这种计算起来比较简单。  

但是实际情况中很多投资现金流是不规律的，比如下面的投资明细表，记录了每次现金流出流入的金额和日期：

现金流的时间跨度不一样，金额也不规律，想要知道这个投资的内含报酬率，就不是前面的RRI函数能计算的了。

不过利用XIRR函数，计算这种无规律现金流的内含报酬率，同样非常方便：  

> 内含收益率 = XIRR( '投资明细表' , \[现金流\] , \[日期\] )

上述投资的内含报酬率为24.87%。

关于财务函数就简单介绍这几个，更多财务函数可以在官方文档中了解，其实这些函数都不复杂，先熟悉这些函数的语法，弄清楚他们的作用和对应的参数，然后将相关财务信息放到指定的参数位置上，就可以直接得到需要的结果。
