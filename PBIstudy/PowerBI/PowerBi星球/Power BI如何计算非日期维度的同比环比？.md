---
create_date: 2020-11-23T23:46:16 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI如何计算非日期维度的同比环比？
source: https://mp.weixin.qq.com/s/KnjQYHsh9lDwipbxxlhS3A
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

对于自然日期维度的业务数据，在PowerBI中可以轻松的使用时间智能函数来进行各种时间指标的计算（[各种时间指标的度量值，让你一次看个够](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069739&idx=1&sn=e8a57761fe68cf5f3a92ed811c314c59&chksm=8e0c4fbcb97bc6aa7391500817c58416077b696acc892b4cb58024d0f23a5031dec2cfd7c14b&scene=21#wechat_redirect)），但如果不是按标准的日历，甚至都没有日期维度，该怎么计算呢？

比如下面这个业务数据，每个订单时间并不是按日期来区分的，而是按期间来划分，一年划分为6个期间，分别为P1、P2……

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1SEfFfCBQSaykick8IoZabcNSVJlkRX4GxMBS99lyvz4icrc8kEcxBSlA5WiagOekciaR5NZjLGjcBg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面的数据连个日期维度都没有，如何计算每一期的同比和环比呢？  

其实计算逻辑与日期维度并没有什么不同，日期计算需要有个日期表，非日期的期间计算，同样也需要制作一个期间维度表。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1SEfFfCBQSaykick8IoZabQibjSqYkG9MSnAEe5KbtFeJicxTKkt5tXJ9Q31ltUjM6oNGEnibIrk6mQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

期间维度表与订单表建立关系：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1SEfFfCBQSaykick8IoZabFRU7rosLoZ51ruTkhYCsKHz6vZKia6hXnlMzNiaYheehx2kjYic9dZttg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后根据计算的需要建立几个度量值就可以了。

> 本期收入 \= SUM( '订单表'\[销售额\] ）

上期收入，就是年度相同，期间编号减1的期间的数据，按照这个逻辑写度量值如下：

> 上期收入 =
> 
> VAR year\_ = SELECTEDVALUE( '期间表'\[年度\] )
> 
> VAR period\_  =SELECTEDVALUE( '期间表'\[期间编号\] )
> 
> RETURN
> 
> CALCULATE(
> 
>     \[本期收入\] ,
> 
>     FILTER(
> 
>         ALL( '期间表' ) ,
> 
>         '期间表'\[年度\] = year\_ && '期间表'\[期间编号\] = period\_-1
> 
>     )
> 
> )

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1SEfFfCBQSaykick8IoZabl4ATSibadcAe6Moicv66IoDuPMBVEjl1mdw1MLHNzBpc0pEEKkdq9a3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上图中的结果中，大部分的上期收入没有问题，但是2018年第1期的收入为空，这是因为按照上面的逻辑，第1期的编号减1的期间是不存在的，所以导致这样的结果。  

解决这个问题，可以判断是否为第一期来修正计算的逻辑，不过更简单的办法是，在期间表添加一个连续的期间序号维度，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1SEfFfCBQSaykick8IoZabx5ZM14T4D7ic9yhXrVe2OdydKThGibOQncdHuycHzNibC61VYOsmibKebg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有了这个序号，不用考虑年度，每一期的上期，就是期间序号减1的期间，修正度量值如下：

> 上期收入\=
> 
> **VAR** period\_  =SELECTEDVALUE( '期间表'\[期间序号\] )
> 
> **RETURN**
> 
> CALCULATE(
> 
>     \[本期收入\] ,
> 
>     FILTER( ALL( '期间表' ) , '期间表'\[期间序号\] = period\_-**1** )
> 
> )

这个度量值看起来简单多了，并且计算结果也是我们需要的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1SEfFfCBQSaykick8IoZabL1YbSjJI8cTD5ehqvC64wLnRMA2GK2NS6uU4Ufz2XAYoNFvkAa8a8A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同样的逻辑，计算上年同期的数据，就是期间序号减去6的期间，度量值如下：

> 上年同期收入 =
> 
> **VAR** period\_  =SELECTEDVALUE( '期间表'\[期间序号\] )
> 
> **RETURN**
> 
> CALCULATE(
> 
>     \[本期收入\] ,
> 
>     FILTER( ALL( '期间表' ) , '期间表'\[期间序号\] = period\_-**6** )
> 
> )

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1SEfFfCBQSaykick8IoZabiczqKB7Zibet5iaXCn8vh35oBZku8OkYEAlZnYlT3GeiaXFY5G88icgmnMA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有了上期和上年同期的数据，计算同比和环比就很简单了：

> 环比 \= DIVIDE( \[本期收入\]-\[上期收入\] , \[上期收入\] )
> 
> 同比 = DIVIDE( \[本期收入\]-\[上年同期收入\] , \[上年同期收入\] )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN1SEfFfCBQSaykick8IoZabPoeLB8xdrwnCRzW5uWCFzK4uJ3WNjIvm7rOszTN8zVFfRM0Tdo1VhA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就完成了同比和环比的指标计算。

这篇文章介绍的是一个普遍意义上的时间指标计算思路，无论是可以利用时间智能函数的月度、季度同比环比，还是没有时间智能函数的周、旬等维度的同比环比，都可以按这个思路轻松实现。

如果彻底理解了这种算逻辑，并掌握了DAX表达思路，再碰到各种日历的指标计算，都可以迎刃而解。

之前写过的周分析以及非标准日历，也是同样的计算逻辑：

[学会了这个思路，你也可以轻松进行周分析！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068253&idx=1&sn=ad3b2929ea9a378e42ac0d8e38ef9cff&chksm=8e0c754ab97bfc5ce978455efcbb7ad88f5f7556f009a79cdf43e2741cf4d294f75becbf17fa&scene=21#wechat_redirect)

[Power BI非标准日历的计算思路](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070813&idx=1&sn=70852e62479cfc082b34a63f62ef64dc&chksm=8e0c434ab97bca5c0d7d1ff838a8b1d07f481da3774555a962b0dd76156fd45535a487cfda7a&scene=21#wechat_redirect)  

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，与2k+ 学习者一起成长
