---
create_date: 2022-01-04T13:38:26 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何用 Power BI DAX 计算年度留存客户
source: https://mp.weixin.qq.com/s/ZxKrio4UxAT8MJ-RX_bHIA
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

> 留存客户除了在互联网公司的应用，更是一个通用的问题。

一年过去了，很多企业开始计算，上一年度的客户的留存。我们看这样的问题描述。

假设某公司在 2020 年 12 月有活跃客户 100 人，而在此后的一年中只要有销售额，就算该客户在此后的一年为留存客户。那么，对于试着给出对任何年月的活跃客户计算其在未来一年的留存数以及留存率。

## 活跃客户

活跃客户在不同的业务中的定义也不同，这里我们姑且给出活跃客户的精确定义。如下：

活跃客户，又称某日期区间内的活跃客户，指在给定的日期区间内，有销售的客户，称为活跃客户。其数量为活跃客户数。

## 数据模型

通常，客户表（客户维度）和订单表（交易事实表）以及日期表（日期维度）之间，会构建一个数据模型，大致如下：

请伙伴们记住：

-   永远使用维度表中的字段作为分组字段；而不要使用交易表中的同样字段。
    
-   日期表也必须使用作为维度表的日期表；而不要使用交易表中的日期字段。
    
-   客户是可能重名的，使用客户 ID 作为唯一标识。
    

下面开始来对活跃客户进行计算。

## 活跃客户的计算

其实，活跃客户的概念不难理解，但在结合到表格的时候，却不那么容易，我们需要考虑：

-   单个客户是否活跃；
    
-   某类客户有多少活跃。
    

现在考察单个客户的情况，我们定义一个度量值如下：

```
Customer.活跃.标识 = IF( COUNTROWS( 'Order' ) > 0 , 1 )
```

该度量值的原理是，如果客户维度对交易事实表有筛选，且结果不为空，说明存在交易，则客户是活跃的。这里使用 `COUNTROWS` 表的方式是一种技巧，且考虑了性能的优化问题。

请注意这里的用词：单个客户的情况。

因此，在构造中，必须要求模型设计者将可以表征客户唯一性的标识列作为分组字段，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMqX36z8xFdPn3EcM5GeoRvv5p4e4UjjkwxyiafV3KYMj1UMnNkAzktwxYX8yffcfXg8GE1vEnHRjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到这样的特征，如下：

-   必须有年份和月份作为筛选环境，这是由活跃用户在本场景下的定义决定的。
    
-   使用客户维度的客户 ID 作为分组字段，度量值显示为 “活跃”，数值为 1，表示该客户在当月是活跃的。
    
-   但总计行的 1 并不能给出良好的语义，例如，总计行应该给出总的客户活跃数。
    

值得注意的是，在目前的模式下，如果使用额外的筛选器对客户进行筛选，其效果也是可用的，例如：

如果选定了某个行业，那么该度量值的计算依然有效。

现在的问题是如何处理总计行的问题。关于总计行的处理，我们此前有文章给出了终极方案，此处再做复习，给出考虑了总计行的度量值，如下：

```
Customer.活跃.数量 = SUMX(     VALUES( Customer[CustomerID] ) ,    CALCULATE( IF( COUNTROWS( 'Order' ) > 0 , 1 ) ))
```

该度量值，不仅仅适用于单行客户，还适用于没有客户的总计行。效果如下：

可以看出，此处的总计是正确的。

有了这个计算，我们还可以再提出一个 KPI 单值卡片图，如下：

接下来，要计算的是在所选日期区间未来一年的交易客户情况。

## 日期维度的变换

这里是初学者晋级的一个重要思维切换点，我们此前对日期智能函数的计算也给出了终极思维模式，可以参考此前文章，这里复习如下：

沿着日期维度的计算，其本质是对日期维度的变换。

什么叫日期维度的变换？定义如下：

-   筛选环境中给出了作为筛选的日期区间，称：\[D1,D2\]。
    
-   计算中需要使用另一段日期区间，称：\[D1',D2'\]。
    
-   从 \[D1,D2\] 到 \[D1',D2'\] 的变换就是日期维度的变换。
    

在本案例中，已经筛选了某个年月的区间，但在计算中需要考量的是未来一年的日期区间，有：

-   \[D1,D2\] 为某年月。
    
-   \[D1',D2'\] 为 \[D1,D2\] 随后的一年。
    

即 D1' = D1 + 1，D2' = D1' + 一年。

注意：

一年和 365 日是不同的概念，一年是一个严格的概念，有的年份是 365 日，而有的年份是 366 日，因此，用一年这个概念更加严谨。很多初学者是不区分一年和 365 日这两个概念的，即使其误差从计算结果上可能可以忽略不记，但由于这个概念的不够严谨，可能导致在其他的计算中出现严重问题。

在本案例中，如果要计算某年月随后一年的活跃客户数，可使用以上思路建立度量值，如下：

```
Customer.活跃.数量.未来一年 = CALCULATE(    SUMX(         VALUES( Customer[CustomerID] ) ,        CALCULATE( IF( COUNTROWS( 'Order' ) > 0 , 1 ) )    ) ,    DATESINPERIOD( 'Calendar'[Date] , MAX( 'Calendar'[Date] ) + 1 , 1 , YEAR ))
```

其中，实现日期区间变换的是：

```
DATESINPERIOD( 'Calendar'[Date] , MAX( 'Calendar'[Date] ) + 1 , 1 , YEAR )
```

该变换将清除当前年月日期区间的筛选，同时施加一个未来一年的日期区间的筛选，得到所需效果。

结果如下：

不难看出，客户的活跃有这样的表现：

-   【1】在本月活跃，在未来一年不活跃。
    
-   【2】在本月不活跃，在未来一年活跃。
    
-   【3】在本月活跃，在未来一年也活跃。
    

我们需要进一步来计算留存的客户。

## 留存的客户计算

基于以上的分析，留存的客户，其计算特征如下：

在本月活跃，在未来一年也活跃。

这可以通过不同的 DAX 计算功能组合实现，这里给出常见的集合求交集的方法。如下：

```
Customer.活跃.未来一年留存数量 = VAR vItemsInThisPeriod =FILTER(     VALUES( Customer[CustomerID] ) ,    CALCULATE( IF( COUNTROWS( 'Order' ) > 0 , 1 ) ))VAR vItemsInOtherPeriod =CALCULATETABLE(    FILTER(         VALUES( Customer[CustomerID] ) ,        CALCULATE( IF( COUNTROWS( 'Order' ) > 0 , 1 ) )    ) ,    DATESINPERIOD( 'Calendar'[Date] , MAX( 'Calendar'[Date] ) + 1 , 1 , YEAR ))RETURN COUNTROWS( INTERSECT( vItemsInThisPeriod , vItemsInOtherPeriod ) )
```

以上计算分为三个部分：

-   先计算本期客户列表，返回表。
    
-   再计算未来一年活跃客户列表，返回表。
    
-   再求两个表的交集的数目。
    

如果你想多学习一点，还可以用类似的实现如下：

```
Customer.活跃.未来一年留存数量.2 = COUNTROWS(    FILTER(         VALUES( Customer[CustomerID] ) ,        CALCULATE( IF( COUNTROWS( 'Order' ) > 0 , 1 ) ) &&         CALCULATE( IF( COUNTROWS( 'Order' ) > 0 , 1 ) , DATESINPERIOD( 'Calendar'[Date] , MAX( 'Calendar'[Date] ) + 1 , 1 , YEAR ) )    ))
```

以上方法，针对单个客户进行判断，方法如下：

-   满足本期活跃
    
-   且同时满足在未来一年活跃
    

筛选出所有同时符合上述条件的客户。

这样，整个效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMqX36z8xFdPn3EcM5GeoRvPqibX3FgRgMk1OPROiaRkd29OgkT06zep3Yia0Lm40AEGPhibxbo9h1iaFQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看出两种方法的计算结果完全一致，得到了检验。

## DAX 计算的检验

DAX 的计算是在模型中进行的，这对很多初学者造成困难，因为你根本不知道你计算的正确还是错误。

这里给出的检验方式就是：

用两种方法进行计算，两种方法使用不同的思路或者根本不同的 DAX 函数，来确保它们的逻辑结构不同，如果结果相同，那么两种同时正确，如果结果不同，那么，很可能出现了错误，可以再做检查。

## 留存率的计算

对上表进行简化，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMqX36z8xFdPn3EcM5GeoRvn4mXspjibBmYnTKutMe8mIGjDvcBQM4RHn8OPXcg7fianI8ia4WfQFAgQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中留存率的计算非常简单，如下：

```
Customer.活跃.未来一年留存率% = [Customer.活跃.未来一年留存数量] / [Customer.活跃.数量]
```

这很容易理解。

## 计算的可扩展性

好的度量值设计，是可以兼容不同场景的，例如本案例中的设计除了已经满足了这样的要求外，还可以做到这样的效果，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMqX36z8xFdPn3EcM5GeoRviboZCzQZ4zs5Mic5jjJxZWJ5ndRtuNrK34rUQiawjb8E22bJWnclWERxw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里没有添加任何新的度量值，但对不同行业的活跃客户和留存也给出了计算，请大家观察它的正确性以及自己思考它为什么可以自适应这样的结果吧。

## 总结

DAX 用作数据建模以及计算有着重要的规律和最佳实践，2022 年，我们将带领大家一起从新的维度和视角学习这一套数据分析工具，让你耳目一新。

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

与精英一起讨论 Power BI，验证码：data2021  

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
