---
create_date: 2020-11-02T23:48:56 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI预算分析：预测与预算目标差异比较
source: https://mp.weixin.qq.com/s/Pk08rVFPuIiDad0PS_wU9w
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

上周的文章讲了[PowerBI业务预测](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073605&idx=1&sn=5da4b73e62577965b6d94616ac47934c&chksm=8e0c5e52b97bd74472803d804c8f6e0ee9b1c17ff204a03754f7670dc582aa59c67a3c11f38f&scene=21#wechat_redirect)的几种简易方式，预测完以后，如果想看看预测的结果与预算目标的差距，如何能快速的展现呢？

假设按照上篇文章的第一种预测方式，根据上年数据乘以一定的增长率来作为本年的预测数据，上篇文章已经预测了每天的业务数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOlntoTGkCiapnBAGzEcYCB4rrD9gxgKibbOt4dZbz6W3HMiaBVq765l9b3ZEfHMXcsVFVIxJuLfVBibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想看看全年的预测数据与预算目标的差距，就需要计算出最后一个业务日期之前的实际数据，与尚未发生业务的日期的预测数据之和。  

其中，全年预算目标与实际业务数据的比较，前面的文章已经介绍：[Power BI预算分析：预算实际比较](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073470&idx=1&sn=f6488ff805a4a1a1d9c29cbdd4de0622&chksm=8e0c5929b97bd03fda6ea3908dfc2dc2c1956b5a354947b8f3ac8c7289b450611554c5879854&scene=21#wechat_redirect)

先将实际数据的累计与预算对比：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOlntoTGkCiapnBAGzEcYCB4BBhmWgyvuUCzv0PrjlbHJ06aKLaBNWU02bmP7TTPob24kJetn6gOQw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为是要看全年的预算与预测的对比，所以这里不再只显示到最后一个业务日期的数据，而是显示全年的数据。至于未发生业务期间的累计数，就涉及到本文的重点了。

新建度量值：

> 全年预测YTD \=
> 
> IF(
> 
>     MAX('日期表'\[日期\])>=\[最新业务日期\],
> 
>     SUMX(
> 
>         DATESYTD('日期表'\[日期\]),
> 
>         \[收入 实际\]+\[收入 预测1\]
> 
>     )
> 
> )

因为累计的预测只显示在未发生的期间，所以用IF做了判断，如果在未发生的期间，就将截止当前日期的实际发生累计数，与预测累计数相加，也就是本年至今的累计数。

效果如下：

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

从上图可以看出，在预测期间，假如同比增长10%，在年底未达成预算目标，为了显示差距是多少，还可以写个差异的度量值：

> 预测 预算差异 = 
> 
> CALCULATE(
> 
>     \[全年预测YTD\]-\[收入 预算 YTD1\],
> 
>     '日期表'\[日期\]=DATE(2020,12,31)
> 
> )

做个卡片图放到报表中，就可以直观看出差距是多少了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOlntoTGkCiapnBAGzEcYCB4iapT8gvFRibkficccK3w3pdbwx6xemwb9ODOdQf6dURocXQRpic6ib6xSJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当增长率是10%的时候，差距是49,120，那么增长率应该达到多少，才可以达成预算目标呢？利用参数来模拟一下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOlntoTGkCiapnBAGzEcYCB4XDrn9icsxXy4IHQqO4ib4f9Kwh5Rjk1gkVshJ98GKJtzEe4cBRj4RgLQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

利用上图可以直观的看出，增长率越高，全年预测数据越接近预算目标，最终模拟的结果是，未来期间的业务同比增长大约是45%，才能完成预算目标。

这也是一个模拟分析的例子，其中几种预测方式也都可以同样的方法来展示。这样我们就可以轻松看出预测结果相对预算目标的偏离程度，以便进行及时的调整。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和2.6k+ 学习者一起成长
