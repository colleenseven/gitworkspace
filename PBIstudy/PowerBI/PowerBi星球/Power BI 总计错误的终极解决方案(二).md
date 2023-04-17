---
create_date: 2020-09-04T20:40:25 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI 总计错误的终极解决方案(二)
source: https://mp.weixin.qq.com/s/-hDULGTGDU543TKITmeLYQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

关于PowerBI总计行不等于明细行的问题，之前曾写过一篇文章，专门解释了原因并提供了解决方案：[PowerBI 表格总计错误的终极解决方案](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068768&idx=1&sn=e74b48b6b29465ec79784cfff320a7b5&chksm=8e0c4b77b97bc261ba080b8532b29b7853fc0f80607c783a8e7565139e980be308d325fa6b4e&scene=21#wechat_redirect)

但在实际应用过程中，仍然会碰到这个简单的解决方案解决不了的其他情形，主要的问题来自于，当上下文超过一个字段时，总计行仍不正确的问题。

这里收集了星友们遇到的几种情况，将解决方案进一步拓展。

示例模型如下，一个订单表，三个维度表，其中日期表和产品表与订单表建立了关系，仓库表没有与订单表建立关系。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOfZyJZPrZ7rfvialjs6a37icmundgEhibGicdXibdYdEzcMJrTN615iaQxkhL88PwLwzh8NvzMPHu3oc9w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**需求：计算每种产品的客户数量，并且要求总计行的结果等于每种产品的客户数量之和。**  

先建立一个基础度量值：  

> 客户数 = DISTINCTCOUNT( '订单表'\[客户姓名\] )

结果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOfZyJZPrZ7rfvialjs6a37icO4KPd7JoIEQcNhHDxXRMmiaycJiadoClXlpS0iavxMUVr3WQuxnHE19bQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从这个结果来看，总计是179，明显小于明细之和202，这也可以理解，毕竟不同产品的客户或许有交叉的情况，这样，总体的客户数就是很可能少于每种产品客户数量的简单相加。  

这里我们不考虑这个具体逻辑，就是想按照要求，让总计行等于明细行之和，怎么做呢？

利用上篇文章的解决方案，再写个度量值：  

> 客户数 优化1 =
> 
> SUMX(
> 
>     VALUES( '产品表'\[产品名称\] ) ,
> 
>     \[客户数\]
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOfZyJZPrZ7rfvialjs6a37ic4E6gPwUG91C7XP9CKdY33Dwc9ICSarazBKok7sZ3iaVUZYiabK4Rw5nA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样总计行就修正为明细行之和了。

上面是只有一个产品名称字段的情况，这个解决方案没有问题，但是如果上下文超过一个字段，并且几个字段可能来自于不同的维度表，这个总计会变成什么结果呢？

下面分几种情况来介绍。

**1.上下文的字段来自于同一个维度表。**

在这个矩阵中，再增加一个产品类别字段，与产品名称均来自于产品表：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOfZyJZPrZ7rfvialjs6a37icqBWhwJyXGo8qhyIuGiaZBpaHr4NTNaibXyHUmkDc4xe08ESG5L0ZFbOA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从这个结果来看，小计行和总计行的结果，均等于明细行之和，所以这种情况下，依然可以用上篇文章的解决方案。

**2.上下文的字段，来自于不同的维度表，并且均与事实表建立的有关系。**

假如在上面的矩阵基础上，在【列】中放一个月份字段，从上面模型可以看出，产品表与日期表，均与订单表建立了关系，这种情况下，用上面的度量值\[客户数 优化1\]是什么结果呢：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOfZyJZPrZ7rfvialjs6a37ic8bkTbBJ7kcyhoFjTibicxaXIUAqBmgv6JicSDpjqy9COxcTlLLTm92thg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看出每一列的数据是正确的，因为度量值\[客户数 优化1\]已经考虑了产品名称，但是没有考虑月份，在某些行上的汇总就不正确了，如上图的标记，因为不同月份的客户同样会有重复的情况。

如何让月份的总计也等于每个月的数据之和呢？

这里给出第二种解决方案：

> 客户数 优化2 =
> 
> SUMX(
> 
>     SUMMARIZE(
> 
>         '订单表',
> 
>         '日期表'\[年度月份\],
> 
>         '产品表'\[产品名称\]
> 
>     ) ,
> 
>     \[客户数\]
> 
> )

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOfZyJZPrZ7rfvialjs6a37icHKZbjwWmRqWlRtPLquyMjQ9VY8q3GwzpZhib1CkyuAK0hpbMghO17Vw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

无论是小计、列总计还是行总计，均等于明细之和。

这种是最常见的情况，并且可以替代第一种方案，在SUMMARIZE里只放一个字段即可。

> 客户数 优化1 =
> 
> SUMX(
> 
>     SUMMARIZE(
> 
>         '订单表',
> 
>         '产品表'\[产品名称\]
> 
>     ) ,
> 
>     \[客户数\]
> 
> )

**3.上下文的字段，来自于不同的维度表，并且与事实表没有建立关系。**

如果将仓库表中仓库地点，拖拽到【列】中，结果会是什么样呢？从上面的模型可以看出，仓库表与订单表没有建立关系。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOfZyJZPrZ7rfvialjs6a37icLo4KPUwsXnpActekH4U1aVTHZebqwhVDF08dI7gNaiaRDYeWq1RQvWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为仓库表没有与订单表建立关系，所以每个仓库数据都一样，并且行总计也是与每个城市数据相同。

这种需求逻辑非常少见，但即使如此，如何让行总计也等于明细之和呢？

这里给出第三种解决方案：

> 客户数 优化3 \=
> 
> SUMX(
> 
>     CROSSJOIN(
> 
>         VALUES( '产品表'\[产品名称\] ),
> 
>         VALUES( '仓库表'\[仓库\] )
> 
>     ) ,
> 
>     \[客户数\]
> 
> )

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOfZyJZPrZ7rfvialjs6a37ic0ADbnxaYmo1Q8o1GWLBPIqt2o8DXiaI9KRvFRNmR6ofU0TgRianBicnJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

依然做到了小计、列总计和行总计均等于明细之和。

**总结**

根据具体的情况，为了使总计等于明细行之和，分别优化度量值如下：  

**1.矩阵的行列字段只有一个，或者有多个字段，但来自于同一张表时：**

> **总计优化方案1** \=
> 
> SUMX(
> 
>     VALUES(维度表\[字段\]),
> 
>     \[明细行正确的度量值\]
> 
> )

**2.**矩阵的行列字段**来自不同的维度表，但均与事实表建立关系时：**

> **总计优化方案2** \=
> 
> SUMX(
> 
>     SUMMARIZE(
> 
>         '事实表',
> 
>         '维度表1'\[字段1\],
> 
>         '维度表2'\[字段2\]
> 
>      ) ,
> 
>      \[明细行正确的度量值\]
> 
> )

**3.****矩阵的行列字段****来自不同的维度表，但未全部与事实表建立关系时：**

> **总计优化方案3** \=
> 
> SUMX(   
> 
>    CROSSJOIN(
> 
>         VALUES(  '维度表1'\[字段1\] ),
> 
>         VALUES(  '维度表2'\[字段2\] )
> 
>     )
> 
>      \[明细行正确的度量值\]
> 
> )

其原理都是根据矩阵的行列字段，利用DAX表函数构造出一个与矩阵结构相似的虚拟表，作为SUMX的第一个参数。

**然后利用SUMX的迭代特性，结合筛选上下文和行上下文的共同作用，**当这个度量值位于明细行时，明细行把SUMX的第一个参数表筛选为与外部上下文一致，SUMX的计算结果就是第二个参数表达式的正常计算结果；如果处于总计行，SUMX正常迭代，将各明细行的数据累加。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.3k+ 学习者一起成长
