---
create_date: 2020-10-16T20:32:21 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI可视化技巧：柱形图动态显示预算实际
source: https://mp.weixin.qq.com/s/VqwtSu_nPoFgTDshDXyf1A
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

之前碰到多次星友提出类似这样的问题：展示预算和实际数据时，如果是已经发生的月份就显示实际数据，未发生的月份显示预算数据，并用不同的颜色区分，这应该怎么做呢？

接着前面关于[预算分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073470&idx=1&sn=f6488ff805a4a1a1d9c29cbdd4de0622&chksm=8e0c5929b97bd03fda6ea3908dfc2dc2c1956b5a354947b8f3ac8c7289b450611554c5879854&scene=21#wechat_redirect)文章的介绍，如果直接把实际和预算数据放到簇状柱形图中，效果是这样的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMia8EB8gMYl55GvR3cSyaFO4xMdmicTBwoU9E1Xm3GoRw6IibNkhok3Yryf9ck0hNAS5ib3qjuWAV1ibA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

现在打算实现的效果是，已经发生完整业务的月份就只显示实际数，未发生业务的月份只显示预算数。  

比如在这个案例中，完整的业务月份是到9月份，如何让1-9月显示实际数据，而第四季度的三个月显示预算数据呢？并且用不同的颜色表示预算和实际数据。

可以构建两个度量值来实现：

> 收入 实际 = 
> 
> IF( MAX( '日期表'\[日期\] )<= \[最新业务日期\] , \[收入\] )
> 
> 收入 预算 = 
> 
> IF( MAX( '日期表'\[日期\] ) > \[最新业务日期\] , \[收入 预算分配\] )

这两个度量值都是利用当前上下文的最大日期与\[最新业务日期\]比较，\[收入 实际\]度量值的判断逻辑是，如果是已发生业务的完整月份，显示实际数，否则返回空值；而度量值\[收入 预算\]的逻辑正好相反。

对于不完整的业务月份，在这个柱形图中，上下文是月份，MAX返回当月的最后一天，只要 \[最新业务日期\]不是最后一天，当月就不完整，只有\[收入 预算\]会返回预算数据。

利用这两个度量值生成堆积柱形图，就是目标效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMia8EB8gMYl55GvR3cSyaFOMOEYXj2Kib0gFXcAOnQEIZAj5m8ZEueHUmzSd3krLibDhQpAzcHoU8Iw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当10月业务发生完以后，该柱形图会自动将10月份的数据变更为实际数据，并用橙色显示。

更进一步的，还可以创建一个月份[参数](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067672&idx=1&sn=1a141b81b4e20f83cabf410164f55974&chksm=8e0c778fb97bfe9904d988eb9972b26436c260e575d008d1414076b86df997fee74dc559ec73&scene=21#wechat_redirect)，将上下文的月份直接与参数比较，来动态显示任意一个月份分割的实际和预算数据。  

关于如何建参数不再介绍，如果不熟悉你可以参考这篇文章来了解：[创建PowerBI「参数」轻松搞定动态分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067672&idx=1&sn=1a141b81b4e20f83cabf410164f55974&chksm=8e0c778fb97bfe9904d988eb9972b26436c260e575d008d1414076b86df997fee74dc559ec73&scene=21#wechat_redirect)，这里直接用建好的参数来修改上述度量值：  

> 收入 实际 = 
> 
> IF(MONTH(MAX('日期表'\[日期\]))<=\[月份 值\],\[收入\])
> 
> 收入 预算\= 
> 
> IF( MONTH(MAX('日期表'\[日期\]))>\[月份 值\],\[收入 预算分配\])

然后利用参数切片器就可以进行动态切换：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMia8EB8gMYl55GvR3cSyaFO74YLl8J9saSLpMxCkWgzduOHerS02yIicLOicvaKUWD1UX6r4libjialFA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

甚至可以用个播放器来自动循环展现实际和预算数据的变化：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMia8EB8gMYl55GvR3cSyaFOcQXzbyloIJa1hZwKE9kOiaMEwjRR7GsqPFf79DvfYC7HTjWFu5FShZg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

当然这里这样做并没有太大意义，主要想要表达的是，这种技巧并不只是适用于预算分析，当你有类似的动态展现需求时，都可以参考这种思路来实现。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.5k+ 学习者一起成长
