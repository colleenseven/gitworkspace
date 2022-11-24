---
create_date: 2022-06-28T11:48:09 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI DAX 递归问题如何解 - 比例型
source: https://mp.weixin.qq.com/s/QSr2nHxxKfT3Nnr1gMy7kw
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月28日 20:00 直播

PowerBI

视频号

有很多小伙伴常常问到含有递归特性的 Power BI DAX 计算问题，这在 DAX 中应该如何解呢？

本文来阐述【比例型】的解决方案。

## 问题场景

已知每年的预期增长率如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOWSJJonAGpDX35OdxRzicE2wSgoJFLtJCQUHPAMDM0dDEMUOHLMyicZKYuIJibRVdP1JJAJ5qVegXuQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以及每年的销售额，如下：

分别求各年的预计销售额。

## 问题分析

对于预期增长率表，其含义为：

当前年份相对前一年份的预期增长率。

也就是说，

对于 2022 年，要想求该年的预计销售额，就需要先知道 2021 年的预计销售额，再乘以预计增长率；

对于 2021 年，要想求该年的预计销售额，就需要先知道 2020 年的预计销售额，再乘以预计增长率；

对于 2020 年，要想求该年的预计销售额，就需要先知道 2019 年的预计销售额，再乘以预计增长率；

…

进而，可以归纳为这样的规律：

对于任意所求的元素 X (n)，依赖于对 X (n-1) 的计算。

这就构成了：**递归**。

## DAX 的递归限制

DAX 并不提供对递归计算的天然支持，导致一些问题无法自然得解。Excel 中可以轻松解决的问题，在 DAX 中变得很复杂。例如：已知初始月份的存货以及每个月的出货，进货数据，求每个月的月末库存，也将导致递归问题。

在 Excel 中，可以在某行直接引用上一行的元素，实现递归。

在 DAX 中，却无法直接引用上一行元素，导致无法实现递归计算。

## 递归的特殊形态

递归存在一些特殊形态，通过数学运算的等价性，可以在某些场景中给出结果。

例如，这里给出比例型递归问题的通用 DAX 解法。

## 比例型递归

设：X (n) = X (n-1) \* A (n-1)，其中 A (n-1) 为已知序列 A (n) 中的元素。

则：

X(n) / X(n-1) = A(n-1)

X(n-1) / X(n-2) = A(n-2)

…

X(1) / X(0) = A(0)

上述等号左右相乘，则进一步有：

X(n) / X(n-1) \* X(n-1) / X(n-2) \* … \* X(1) / X(0) = A(n-1) \* A(n-2) \* … \* A(0)

整理，得：

X(n) / X(0) = A(n-1) \* A(n-2) \* … \* A(0)

则：

X(n) = X(0) \* ( A(n-1) \* A(n-2) \* … \* A(0) )

可见，对于任何 X (n)，已经化解为对已知序列的计算。

具体实现如下。

## DAX 合并模式

首先，来合并一个待预测的序列，使用标准的 DAX 设计模式，如下：

```
Year.Combine = SUMMARIZE(    FILTER(        UNION(            VALUES( GrowthList[Year] ) ,            VALUES( Sales[Year] )        ) ,        NOT ISBLANK( [Year] )    ) ,    [Year])
```

接下来就需要对这个序列计算。

## 递归计算

由于 DAX 不支持递归，但可以用已经推导出的公式替代，化递归为聚合运算，公式如下：

X(n) = X(0) \* ( A(n-1) \* A(n-2) \* … \* A(0) )

若某元素有已知值对应则取值。

若某元素没有已知值对应，则按照上述公式计算。

设 X (0) 是最后一个已知的元素。

则有：

```
Sales.FC = VAR vCurrent = SELECTEDVALUE( 'Year.Combine'[Year] )RETURN    IF(         // 对于已经发生的年份        vCurrent IN VALUES( Sales[Year] ) , SUMX( Sales , ( Sales[Year] = vCurrent ) * Sales[Sales] ) ,        // 对于尚未发生的年份        VAR v0  = MIN( GrowthList[Year] )        VAR vX0 = SUMX( Sales , ( Sales[Year] = v0 ) * Sales[Sales] )        VAR vN  = vCurrent        VAR vXn = vX0 * PRODUCTX( FILTER( 'GrowthList' , [Year] >= v0 && [Year] < vN ) , [Growth] )        RETURN            vXn    )
```

如果想同时看到计算的过程以便于理解，则可以加入一个测试逻辑，如下：

```
Sales.FC.Debug = VAR vCurrent = SELECTEDVALUE( 'Year.Combine'[Year] )RETURN    IF(         // 对于已经发生的年份        vCurrent IN VALUES( Sales[Year] ) , SUMX( Sales , ( Sales[Year] = vCurrent ) * Sales[Sales] ) ,        // 对于尚未发生的年份        VAR v0  = MIN( GrowthList[Year] )        VAR vX0 = SUMX( Sales , ( Sales[Year] = v0 ) * Sales[Sales] )        VAR vN  = vCurrent        VAR vXn = vX0 * PRODUCTX( FILTER( 'GrowthList' , [Year] >= v0 && [Year] < vN ) , [Growth] )        RETURN            // vXn            // Debug:            FORMAT( vXn , "0.0" ) & " = " &             FORMAT( vX0 , "0.0" ) & " *             ( " & CONCATENATEX( FILTER( 'GrowthList' , [Year] >= v0 && [Year] < vN ) , [Growth] , "*" ) & " )"    )
```

这样就得到了最后的效果。

## 测试效果

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOWSJJonAGpDX35OdxRzicE2Mc3Eyw3SfbJuvChBBia6Rm70997XJ6V6YP0ZE1UdxtX3Cvoicwz8T7QA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 💡注意
> 
> 测试的公式括号中的参数是没有顺序的，但不影响结果。可以控制顺序，但此处不是必须的。

## 总结

虽然 DAX 并不支持递归，但对一部分具有特点的递归计算，可以化解成数列聚合运算模式，本文给出了这方面的探索和示范。在滚动预测，存货，库存，余额等场景中均可以使用。

请注意，在实现 DAX 公式时，是严格按照数学公式对照实现的。另外，给出了一种合并数据的标准设计模式，以及现场测试的显示模式。

该递归化解的方法，可以解决一大票常见的 DAX 递归问题，但并不能解决任意递归问题。本例的特点在于第 n 项与第 n-1 项是一种单纯的比例关系，对于复杂的函数运算关系，则很可能无法求解。但我们更关注实际的业务问题，如果大家有这方面的例子，也欢迎探讨。

  
精彩节目，错过可惜

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月28日 20:00 直播

PowerBI

视频号

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

点击“阅读原文”进入学习中心

**↙**
