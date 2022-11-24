---
create_date: 2022-09-28T11:35:09 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 中处理重复排名，展示TOPN
source: https://mp.weixin.qq.com/s/QWOf4W0AzLAthUhjexNkmg
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

业务中，常常需要显示 TOP N 的排名前几的产品（或门店，区域）和销售额（或其他指标）。尴尬的问题在于，如果指标的大小一样，会出现重复的元素的情况。例如：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LP4Boy2eiaNY9YMMJ080IjAZqS8LD4lA0zw23nYDc6mBic0fTjLGQf3lCQIPyS6aYEhVpxLQAcOKE8w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果只想显示前三，应该是：K，F，G。其中，F 和 G 是 30 个 60 中的任意两个即可。而不再显示后续元素，要实现的效果如下：

这该怎么做呢？

## 数据模型

数据模型上，没有什么特别的，这里用一个简单的模型来举例子。如下：

## 计算

基础度量值，如下：

```
KPI := SUM(sales[销售额])Calendar.YearMonth := SELECTEDVALUE( 'Calendar'[年度月份] )
```

基于基础度量值，来定义 TOP 的方法，如下：

```
TOP1.Text = // 设定需要的 TOP X 元素，例如排名第一的元素VAR xTopXOrder = 1// 以下内容无需改变// 1.从数据中捞取需要的内容VAR tView =    CALCULATETABLE(        ADDCOLUMNS(             SUMMARIZE( 'sales', sales[类别] ) ,            "@KPI",[KPI]        ) ,        ALLSELECTED()    )// 2.按照KPI和Item名称做两种初步排序VAR tViewRank =    ADDCOLUMNS( tView ,        "@RankByKPI"  , RANKX( tView , [@KPI] ) ,        "@RankByItem" , RANKX( tView , [类别] )    )    // 3.按照初步排序做一个总排序，主排序按照KPI来，当KPI值相同的时候再按名称排序VAR tViewRankRank =    ADDCOLUMNS( tViewRank ,        "@RankTotalValue" , [@RankByKPI] + [@RankByItem] / 100 ,        "@RankTotalOrder" , RANKX( tViewRank , [@RankByKPI] + [@RankByItem] / 100 , [@RankByKPI] + [@RankByItem] / 100 , ASC )    )    // 4.找出与当前TOP相匹配的记录VAR rItem = FILTER( tViewRankRank , [@RankTotalOrder] = xTopXOrder )RETURN     CONCATENATEX(         rItem ,        [类别] & ":" & [@KPI]    )
```

算法的解释已经在以上公式中描述了，这里就不再另外解释。

这里用到了很多重要的约定，设计模式，技巧。分别说明一下。

## 约定

在数据模型中，会遇到四种情况：

-   值，如：1，约定定义为 VAR xItem = xxx，以 x 为前缀表示是一个值。
    
-   列表，如：一个产品序列，约定定义为 VAR lProducts = xxx，以 l 为前缀表示是一个列表。
    
-   记录，如：某个表的一行，约定定义为 VAR rItem = xxx，以 r 为前缀表示是一个记录。
    
-   表，如：某个表，约定定义为 VAR tViewTable = xxx，以 t 为前缀表示是一个表。
    
-   计算列命名时用 “@” 做前缀。
    

很多初学者问如何化简学习难度，好的习惯和约定就是一种重要的方法。

约定不是必须的，有人喜欢把变量的名字起名为：

```
VAR a = ...VAR b = ...VAR xiaoShouJinE = ...
```

可以是可以，但并不优雅。为啥要优雅？因为，优雅就在那里。

## 设计模式

在计算中，其通用套路就是一种设计模式，描述为：

步骤一，从高度压缩的数据模型中取数，套路为：

```
VAR tView =    CALCULATETABLE(        ADDCOLUMNS(             SUMMARIZE( 'sales', sales[类别] ) ,            "@KPI",[KPI]        ) ,        ALLSELECTED()    )
```

步骤二，针对步骤一获得的数，进一步做运算，套路为：

基于步骤一的结果，临时固化，此结果不再改变，也就意味着，不再收到筛选上下文或上下文转换的影响，极大降低了使用难度。

通过运算得到最终结果。

## 技巧

这里使用的技巧包括：

-   视图层计算设计模式
    
-   不断新加列，且利用前序结果
    
-   RANKX 的技巧
    

## 总结

PowerBI 中学习 DAX 是有很好的模式可以遵循的，可以大幅度缩小学习曲线，也可以让业务人员真正把 DAX 和 Power BI 作为工具，而不用具体钻研它。这些在《BI 真经》中都有系统讲解，这里就不再重复了。

当然，如何将整个套路更加简化，的确有更直接的感悟，会在另外的文章中分享。

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，可以下载本文案例。

**Power BI 终极系列课程《BI真经》**

[

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

点击“阅读原文”进入学习中心

**↙**
