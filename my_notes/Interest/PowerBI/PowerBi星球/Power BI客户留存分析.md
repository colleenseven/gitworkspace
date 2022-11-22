---
ZK: Origin
notes: True
aliases: null
create_date: 2022-04-15T11:54:57 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: Power BI客户留存分析
source: https://mp.weixin.qq.com/s/CyILhnBByvw_ng3flvBiMQ
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

DAX:: COUNTROWS,VALUES,SELECTEDVALUE,CALCULATETABLE,VALUES,DATEADD,INTERSECT,DIVIDE, ADDCOLUMNS, ALL, MIN, ALLEXCEPT,FILTER,CONTAINS

之前曾经介绍过[流失客户分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068996&idx=1&sn=a0d5537587f73a2a77ffa62230f05a4f&chksm=8e0c4853b97bc145a3725df97734115f949ba1f438881e3ca5c1af4fbf6f01d3a9a24e27a107&scene=21#wechat_redirect)，与其相对应的，还有个<mark style="background: #FF5582A6;">留存客户分析</mark>，也就是经过一段时间，依然活跃的客户；客户留存率经常用来<mark style="background: #FF5582A6;">衡量市场营销活动的质量</mark>，这篇文章就来介绍一下如何用PowerBI进行留存分析。  

以这个简易的订单模型为例，一个订单表和两个维度表，模型如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwWaibPiaCSspqenVNEnPKYOXdMzhuugXHJmQUbIH5TARW5kXicly4pXr8g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

通过这个模型，计算出每期的客户数量很简单，写个度量值即可：

> 客户数 = COUNTROWS(VALUES('订单表'\[客户姓名\]))

**活跃客户留存分析**

如果你想查看本月下单的客户中，在1个月后还有多少客户购买、2个月后还有多少客户……？这就是一种<mark style="background: #FF5582A6;">活跃客户的留存分析。  </mark>

对于1个月后、2个月后……这种分组，首先需要建个分组表（方法参考：[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)）：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwSGtlZ2quetezU6zFIicNMT0pz8GIwDN4p54y8XNJw2SJ3jTy5jC3ABg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这个分组表不需要与模型中的其他表建立关系，在这个表中，也<mark style="background: #FF5582A6;">添加了“本月”的类别，这样不仅能显示N个月后的数据，也能同时显示本月数据，方便放到一起比较</mark>。  

并且分组表的序号非常有用，这里不仅可以对类别进行按列排序，还可以利用它来控制月份，留存客户数的度量值如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwKobcsLUNTjichTwcK3DMrmdSqtB0LQIpSXTia8icfDibiancUTBH4WIrrhg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这个逻辑很简单，就是<mark style="background: #FF5582A6;">先找出本月的客户列表，然后根据留存分组表的序号，利用DATEADD函数移动到对应的月份，筛选出移动N月后的客户列表，然后统计二者交集的行数，就是N月后的留存客户数。</mark>

将年度月份放到矩阵的行、留存分组表类别放到矩阵的列，展示这个度量值的结果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwD0cJPTw0RjJoJA1gVQbd9sA3emGrhTOX0IldBjxdZsenptFdt7Tzag/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

因为模拟数据是截至到2020年底，所以当前月的N个月后，如果晚于2020年12月，就不会再有数据，所以对角线右下方的数据都是空值。

有了留存客户数，还可以计算出留存客户率：

> 留存客户率 \= DIVIDE(\[留存客户数\],\[客户数\])

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwa20r2wGwak1l2Vfj763oxycMWkEWSdUKQqR0CicAxiatYia3pp9rYJQKQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

为了更直观看出留存客户分布的规律，可以对这个矩阵的数据设置背景色：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwsdprmQzwpR8UUIsHwTdjHiae6gm8cb9TXaDEftx3EZckpvvL3x62OPA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

渐变背景色效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwUWrS6Lsw6YSksWcxweUeVhKiahTRF6TQf4OyDoFB4JOwWm8CQcMn1GA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

以上是对本月所有客户的留存分析，也就是本月活跃客户的留存分析，实际上，留存分析更多的用途是针新获取的客户，计算N月后的留存下来的客户还有多少，来检验拉新活动的效果。

**新客户留存分析**

关于新客户的计算逻辑，可以参考之前关于新客户分析的介绍：

[如何使用Power BI计算新客户数量？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068461&idx=1&sn=7d0cc28760d0afd4f7c1e53e3c319437&chksm=8e0c4abab97bc3acca7a5e9b89d85ac48a5484d9bc2fc3709519db7d955adc2b3e838c51995e&scene=21#wechat_redirect)  

计算每月新客户的度量值是这样写的：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwdicbFLOGvZM322gAwg9Uk5WXus7eFEsNaIt8RbIvD8rGSpaW7cNU1Cg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于新客户在N个月以后的留存数量，同样可以利用DATEADD函数移动到N月后，看看这些新客户还有多少是活跃的，将这个新客户度量值的最后一行稍微改一下即可：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwZtTN7icTSAspibDrQVLFyjCaPxjiakhuZicIKBl19cIIhvuodZ31JvmZgw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这样就计算出了新客户在N个月以后依然有交易行为的客户数量，矩阵展示如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDweuDcVicjw614M7e4e6ovBqfyAtPwxRTOBqmtTiaCRfVXic6GiaVVul1mfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

有了新客户的留存数量，就能很方便的计算新客户留存率：

> 新客户留存率 \= DIVIDE(\[新客户留存数\],\[新客户数\])

设置背景色后的留存率展示效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8ZXiaGSMIrC4BJILwPTEDwcMfeTdEqiaFTU2bicyvtfENXmicMV6oiaWib0JysbFsnTx62JEPjc1ePHvg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

至于留存率的结果，并不都是随着时间的流逝，留存率越来越低，还要结合产品更换周期、市场推广活动等综合考虑，来解释和发现留存率的真实规律。

以上就是对活跃客户以及新客户的留存分析思路，如果你想看看某一期间留存的是哪些客户，你也可以利用这篇文章的方式显示所有的留存客户的名称：

[Power BI如何动态展示表？送你两种方法](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074639&idx=1&sn=03b003d199f754794c0bac8af15c50e0&chksm=8e0c5258b97bdb4e0aa92667a047bca5c7705f86a6c2b4ac66e3eefc171ca95e6891a433ecff&scene=21#wechat_redirect)  

本文示例是按月为周期的留存分析，你可以根据需要扩展为其他粒度，基本逻辑是类似的。

