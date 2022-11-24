---
create_date: 2022-04-29T13:16:36 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 如何准确计算门店数
source: https://mp.weixin.qq.com/s/Jg232rYhbcoELMy5l9hp7A
author: 艾欧里亚zheng
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

门店数是企业经营最基础的指标，在一定程度上代表着市场占有率，也是计算单店营业额（店效）的基础。

在讲解门店数的计算逻辑前，首先聊下一家门店，从开店到撤店所经历的几个重要时点。一家门店装修完成，就可以择日开张营业，营业第一天就是开店日期。在正常经营了几年后，门店的装修及道具需要升级改造，或是由于经营业绩原因，需要扩大或缩小营业面积，门店进入重装阶段，这样会有重装开始日期及重装结束日期。又经过一段时间，门店周边客流较差，或是房租到期续签租金过高，老板决定关店。做了几场特卖活动，甩了一部分库存后，门店正式关店。门店不产生销售的日期，就作为撤店日期。门店在系统中的状态，就根据这几个阶段，分为装修中、营业中、重装中、撤店。计算门店数时，就要根据以上这些字段确定。图 1 中的门店信息表 Model-Dimstore 记录了门店开业日期、撤店日期及门店状态等关键信息。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LPbD0mRpZp6g227mIv4NazwbAY3xawYMvLQO2hbJd4k4t3yCZZaBW56aU57OszqCMiaoC3pzho1TCw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

图 1 Model-Dimstore 字段信息

门店数包括营业门店数及关店数。本文只计算处于营业状态的店铺数量，有两种业务逻辑：第一种是门店数量不随时间区间的改变而改变，始终显示报表刷新日的门店数量；第二种是门店数量随筛选期间的改变而动态变化，显示筛选期间内处于营业状态的门店数量。

方法 1 公式较为简单，通过门店维度表 Model-Dimstore 中的店铺状态列判断，计算店铺状态为营业中的门店数量，公式如下。

```
门店数 当前 =CALCULATE (    DISTINCTCOUNT ( 'Model-Dimstore'[店铺ID] ),    'Model-Dimstore'[店铺状态] = "营业中")
```

方法 2 公式相对复杂，但具有更强的通用性。通过将筛选上下文的时间区间与门店维度表中的开业日期、撤店日期比较，确定一家门店在筛选期间内是否处于营业状态。当门店在筛选期间之前或筛选期间内开业（开业日期小于等于当前期间的最大值），并且在筛选期间内未撤店（撤店日期大于当前期间的最大值或者撤店日期为空），则判断该门店在筛选期间处于营业状态。

```
门店数 =VAR MaxDate = MAX ( 'Model-Dimdates'[Date] )RETURN    CALCULATE (        DISTINCTCOUNT ( 'Model-Dimstore'[店铺ID] ),        'Model-Dimstore'[开业日期] <= MaxDate,        OR ( 'Model-Dimstore'[撤店日期] > MaxDate, 'Model-Dimstore'[撤店日期] = BLANK () )    )
```

首先，变量 MaxDate 返回当前筛选期间内的最大日期，然后 CALCULATE 函数计算参数 2 和参数 3 的筛选条件，取交集得到最终的筛选条件为开业日期在当期前或当期内，且撤店日期在当期后或者未撤店，满足这两个条件的门店即为在当期处于营业状态的门店，最后对这些门店进行非重复计数，得到当前的营业门店数量。

以上两种方法均通过门店信息表 Model-Dimstore 进行判断，必须保证 Model-Dimstore 的信息准确。我们使用方法 2 对比各个区域各月份门店数变化趋势，如图 2 所示。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LPbD0mRpZp6g227mIv4Nazw52wLtu03BdsTpa9pZHpJTsdgPiaOnX2JzEibg96ztghLQ6RJdJYkWZUg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

图 2 各区域门店数月度变化趋势

接下来进行开关店的分析。开关店涉及的度量值包括本期新增、本期撤店及本期净增门店数。

```
门店数 本期新增 =CALCULATE (    DISTINCTCOUNT ( 'Model-Dimstore'[店铺ID] ),    'Model-Dimstore'[开业日期] IN VALUES ( 'Model-Dimdates'[Date] ))
```

\[门店数 本期新增\] 度量值通过开业日期字段，找到开业日期在当前期间的门店，对这些门店进行非重复计数，即为当前期间新增门店数量。

```
门店数 本期撤店 =CALCULATE (    DISTINCTCOUNT ( 'Model-Dimstore'[店铺ID] ),    'Model-Dimstore'[撤店日期] IN VALUES ( 'Model-Dimdates'[Date] ))
```

\[门店数 本期撤店\] 度量值逻辑结构同上。

```
门店数 本期净增 = [门店数 本期新增] - [门店数 本期撤店]
```

我们使用【瀑布图】对开关店情况进行展示。如图 3 所示，绿色柱子代表增加，红色柱子代表减少，最后的蓝色柱子代表从初始值到终止值的累计变化总量。通过图 3 的【瀑布图】，可以清晰地看到新开店数量在各个月份的增长态势以及各个区域对新开店的贡献情况。除了关注新增门店数，更重要的是关注净增门店数。净增门店代表的是绝对增量，体现的是市场占有率。可以看到 2、3、6、8 月份，虽然都有新开门店，但是门店净增数量都是 0。而营销三区从年初至今，没有新开店，但却撤了 2 家店，净增数量为 -2，说明三区的拓展压力相当大，或是公司在这个区域内战略收缩。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LPbD0mRpZp6g227mIv4NazwRgJ65r97Q3SpUh8dhsZiakp5KleU3TLTqr7ox2y0iaibGOMznYublFqOw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

图 3 新增门店数、净增门店数趋势变化及结构分布

以上是关于门店数开关店的分析。门店数是企业经营分析中最基础的指标，它的计算依赖于门店信息表中的开店日期、撤店日期及门店状态等基础信息。所以及时维护好门店信息表是正确计算门店数的关键。在进行开关店分析时，既要关注新增门店数量，更要关注净增门店数量，及时跟踪各个区域在各月份开店进度达成情况，确保最大限度达成公司的拓展规划。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2022-04-30 周六**

**听本文作者郑老师讲更多零售知识**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LPbD0mRpZp6g227mIv4NazwFSrmhq47OJpfmoFwYUXoKMb7ZNVwjs7icJDZl3JaUTyibB4ur4Fn8WPA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

往期推荐

[

智能零售数字化系列讲座-第一期-运营类指标设计实现与报表设计



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650793250&idx=1&sn=5ee3226b42e77c97a11ee22dc8715ea0&chksm=f18ce533c6fb6c25c8fbee3d418fce76b4430286a1b7c712d6b7922f052a5a80880928fed2ba&scene=21#wechat_redirect)

[

零售智能数字化系列-整体框架



](https://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650793283&idx=1&sn=24849096ae581d980ccd0952bbd920b1&chksm=f18ce552c6fb6c443782e1c6c7eedd9b594ccf5e1ed3fc5f186d2156e32fd1650e87846559c5&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
