---
create_date: 2020-10-11T20:33:11 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI预算分析：预算目标分解
source: https://mp.weixin.qq.com/s/CU1W-j8vEvcJdkYB8AnqNA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

数据有对比才有意义，其中一个比较的维度是与预算目标对比，也就是常说的预算分析。PowerBI的日常工作应用场景有一类就是预算分析，最近就分享一些预算分析的相关内容。

其中一个经常碰到的问题是，预算目标如何分解？因为预算目标一般是年或者按月下达的，但是需要按更细的维度来跟踪，比如每日对比分析，如何把月度目标分解为每日的预算目标呢？

在这个销售分析模型示例中，增加个预算表：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMEEzoUnic78YgnypQOOKgZTTVARjibXMfsbjWA3RxdGJVRjerDUmKkc2Sx9XhOxexticOEewHO5Unng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中预算表的结构是这样的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMEEzoUnic78YgnypQOOKgZT6YOyU1eQZia7vIwUibOHqIU2QtibDerBnRR0BU4ZYWZdKKlwf1eueSH4Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

只有每个月度的预算目标额，如何把这个月度目标平均分解到每一天呢？

这里有个年度月份的维度，不少人直接拿这一列直接与日期表的年度月份列建立关系，但这样做对于需要的结果并没有什么帮助。

这个小需求有很多解决方案，这里给出一个不需要建立关系，只用一个度量值就可以完成的方案。  

先建立基础度量值：

> 实际收入 = SUM( '订单表'\[销售额\] )
> 
> 预算目标 = SUM( '预算'\[销售预算\] )

预算分解度量值如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMEEzoUnic78YgnypQOOKgZTib6LicibW8jDNXjmDyTpCAmkicXjOJ5O2c2fP7BmLhF5Pw1rHVzLqUTnVg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**这个度量值的主要逻辑是，先通过几个变量获取当前上下文的天数、当前月份的天数、当前月份的预算，结果返回当前天数占当月天数的比例，来分解当月的目标。**  

其中获取当月的预算时，因为没有建立关系，用了TREATAS来构建虚拟关系，通过当前上下文来获取预算表中的预算目标。

并且结果只对上下文是日期或者月份时执行该计算，如果上下文是日期，当月天数是31天，该度量值就会返回当月目标的1/31，比如1月的每日预算是1月目标的1/31，2月每日预算是2月目标的1/29：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMEEzoUnic78YgnypQOOKgZTMFnMdjILY7EnnOEHFOLB8loZXdXUmwlGnibUxLI9TwVel6ezlPfoTuQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果上下文是月份和日期，也会返回按照该月的天数占当月总天数的比例来计算预算额：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMEEzoUnic78YgnypQOOKgZT9NMKclgHwOWNA0PdumcBNibEmY5ufbS4RZj9TtEL66lrg0pypKr6pCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个结果还有一个小问题是，没有合计数，并且如果上下文是季度或者年度，也没法计算出结果，那么如何修正呢？  

关于总计修正的问题，之前介绍过，参考：[Power BI 总计错误的终极解决方案(二)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072950&idx=1&sn=fdd3128f59f1797c5a1dad976604f0bb&chksm=8e0c5b21b97bd237c39d1afb7e89f7b453c4fc12b09456aaaca57dd83dbf3e71208752d11b6a&scene=21#wechat_redirect)，这里也可以直接套用：

> 预算 分配 \= 
> 
> SUMX( VALUES( '日期表'\[日期\] ) , \[预算 分解\] )

结果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMEEzoUnic78YgnypQOOKgZTAmxVgIpTmSjUjYSqCxCP7bzSJln1a1N1a0u9bPdL87uibxwjtuhDtMw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样无论在哪个粒度上，预算都能正确分配，可以方便地与实际数据进行同口径比较。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和2.5k+ 学习者一起成长
