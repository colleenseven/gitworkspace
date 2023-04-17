---
create_date: 2020-10-13T20:32:47 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI预算分析：预算实际比较
source: https://mp.weixin.qq.com/s/P-yCy_5UPK1yKEmLL9zPog
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073452&idx=1&sn=31095326ea8a9b64dd1a807303efde4c&chksm=8e0c593bb97bd02d0c32c18253224531c22eaab63806d119723c089b31b6aced96b3ba52e5dd&scene=21#wechat_redirect)介绍了预算目标的分解，将预算分解好以后，就可以与实际数据进行比较了。对比很简单，只需要将实际数据和预算数据的度量值放到图表里就可以了，比如用组合图来展现每日的实际和预算数据，实际值用柱形图表、预算值用折线图表示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqQN8l8GKGyXYlVOd0jq6zTAOmEaUIRrloGqdmlqwD53aharLvHswliaPDibthVibWz6ia9BnFJ9JiclQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以直观看出每日收入的预算完成情况，这里有个问题是，对于还没有发生的日期，不会有实际数据，而只显示预算数据看起来比较奇怪，如何让未发生业务的日期，预算数据也不显示呢？

其实只要先找出业务数据的最后一个日期，并判断当前上下文的日期是否早于这个最新日期就可以了，用度量值判断如下：  

> 最新业务日期 = MAXX( ALL( '订单表' ) , '订单表'\[订单日期\] )
> 
> 是否早于最新日期 = IF( MIN( '日期表'\[日期\] ) <= \[最新业务日期\] , 1 , 0 )

有了这个判断度量值，就可以优化预算的度量值：

> 收入 预算 当期 \= IF( \[是否早于最新日期\], \[收入 预算分配\] )

其中\[收入 预算分配\]就是上篇文章中介绍的分解后预算目标，也是上面组合图中用到的度量值，拿这个新的度量值替换掉它，组合图就会变成这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqQN8l8GKGyXYlVOd0jq6zwRoJaib7fqhcQ3dBNK9h2KcOWK8Vicia5htAuKzM2SJydO9uzyGnmKfdw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

预算数据与实际数据显示的区间完全一致。

如果把月度和季度的字段放到组合图的共享轴中，就可以通过下钻，直观展现这几个维度的当期预算完成情况：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMqQN8l8GKGyXYlVOd0jq6z7brvrvqPdFBgyrHFc2MLndge7oTZR0Iccza662DCnZyZ5wDu6OZ2vA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

上面都是当期数据的对比，并不是看出本年累计是否完成了预算，与预算的差异是多少？

___

为了能清晰的看出本年累计是否完成的预算目标，再建立这几个指标的累计度量值：  

本年累计收入度量值

> 收入 实际 YTD = 
> 
> IF( \[是否早于最新日期\] , 
> 
> CALCULATE( \[收入\] , DATESYTD( '日期表'\[日期\] ) ) )

本年累计预算度量值

> 收入 预算 YTD = 
> 
> IF( \[是否早于最新日期\] , 
> 
> CALCULATE(\[收入 预算分配\],DATESYTD('日期表'\[日期\])))

为了同时进行同期对比，再写个上年同期的累计收入度量值：

> 收入 实际 PYTD \= 
> 
> IF( \[是否早于最新日期\] , 
> 
> CALCULATE( \[收入 实际 YTD\] , SAMEPERIODLASTYEAR( '日期表'\[日期\] ) ) )

这几个度量值都直接判断了是否在业务日期范围内，避免在未来期间显示。

将这几个度量值放到面积图中，就可以直观看出累计收入的预算完成情况以及同期对比情况了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqQN8l8GKGyXYlVOd0jq6zzzRPofPgWh3oibHUYknpicwzTALYy3icVHfcEpNPWlZcgia2Im0g2iaT2eg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

累计收入虽然同比上升，但离预算目标还有一点差距。  

预算对比分析只是用到了最基本的DAX函数，也没有复杂的计算逻辑，PowerBI做起来难度很小，关键是熟悉业务场景，学会用DAX准确的表达，并选择合适的图表进行清晰直观的展现。  

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.5k+ 学习者一起成长
