---
create_date: 2020-10-19T20:31:56 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI可视化技巧：折线图动态显示预算实际
source: https://mp.weixin.qq.com/s/PdgrtsmN2Z9-ZSTeKyQX2g
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073501&idx=1&sn=1af4c410ff552d71a5cb196ec8bd6531&chksm=8e0c5ecab97bd7dc15ba3cccbfab149a704e61b4bc11c6bc186f907a13eb309b6c74710a14b7&scene=21#wechat_redirect)介绍了利用柱形图来动态显示预算实际的做法，本文再介绍一下用折线图实现的思路。

其实用折线图也很简单，需要的字段与柱形图相同，可以直接将柱形图切换为折线图，但切换后的效果变成了这样：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMoaXKadAoAswDibbqicu3qphbnq0zNVevNUkjHOMQYFzkibkdDGYn3wNTf4Idvg2kMy5wVl2xv57Mog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

你会发现，折线有断点，并不是连续的，看起来很奇怪，为什么会这样呢？

这是因为，我们用的两个度量值来制作折线图，这两个度量值就是两条独立的折线，以上图为例，实际收入的折线显示1-9月，在9月份结束，而预算收入的折线显示10-12月，10月才开始，因此从9月到10月之间就成了断点。  

**这个问题在柱形图中不成问题，因为柱形图本身就是一根根柱子分别显示的，并不需要连接到一起，但是折线图这样看就太不美观，那么如何让折线图也像正常一样连到一起呢？**

解决的办法就是让其中一条折线多显示一个月，比如上面的例子中，让实际收入度量值在10月返回预算数，这样前面一条折线到10月才结束；或者让预算收入在9月返回实际收入数，也就是预算折线图从9月份开始。

这里以第二种方式为例：让预算收入度量值，判断时往前推一个月，让它返回实际收入数，修改预算收入度量值如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMoaXKadAoAswDibbqicu3qphkHwhjllPUgVR0A0s2zAIWCuH19FGOtZPGHWN37faQ2HBkf1gttZgcw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为这里还要考虑是否为完整的业务月份，所以稍显复杂，其实逻辑很简单，就是让这个度量值，在正常判断的基础上，往前推一个月来显示实际数据，以便与实际收入的折线结束点保持一致，看起来正好连接在一起。  

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMoaXKadAoAswDibbqicu3qphgOW4mpzibYg0bKQicDVPtT1iauPGiaKqMYGRYHicLia5FFUUSSaRLRWU5KAw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其实在9月，两条度量值都返回了数据，并且同样是实际收入数，所以能实现连接到一起的效果。

与[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073501&idx=1&sn=1af4c410ff552d71a5cb196ec8bd6531&chksm=8e0c5ecab97bd7dc15ba3cccbfab149a704e61b4bc11c6bc186f907a13eb309b6c74710a14b7&scene=21#wechat_redirect)一样，也可以设置个参数来动态显示某个月之前的实际数据以及之后的预测数据。  

度量值修改为：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOs0t89m2vKu9EgjHX3QmFygxgz9mdTqM9Du8so8VTS7sNLtmKibEYu9GTYs4yicGBYBoU3Owm7llkg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里直接判断月份，度量值就简洁多了，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMoaXKadAoAswDibbqicu3qphVqk5BjF9fPibSibQpySQR1fvVoITQnT7PdFic9TZAvf1GFBGDzYgiajSbw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

无论在哪个月，都能显示出之前的实际收入和之后的预算收入，并且折线图是连续的。

这篇文章虽然讨论的是用折线图来展示预算实际，但实际上就为了解决折线图中一个经典的、经常被问到的问题：**如何让折线图分成两个颜色显示，并且折线是连续不间断的？**

这个技巧，你学会了吗？

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.5k+ 学习者一起成长
