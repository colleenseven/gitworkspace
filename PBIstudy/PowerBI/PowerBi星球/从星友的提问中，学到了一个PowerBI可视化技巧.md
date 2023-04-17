---
create_date: 2020-12-12T23:44:09 (UTC +08:00)
tags: 
aliases: null
pagetitle: 从星友的提问中，学到了一个PowerBI可视化技巧
source: https://mp.weixin.qq.com/s/j8I3oz0tvgwidFWI3tBLWg
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

在知识星球社群中，碰到了一个这样的问题，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMTBmAIN2RegHGXTqiawoEfUBl8kOC87VdnwUQ5HfJKGAtZ5NpR1zGhH0R03wJOWibdVicxSIRecC98A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

简单来说，就是如何在两条折线图之间添加柱形图，并用不同的颜色标记中间的柱形。  

刚看到这个问题，感觉实现不了，因为PowerBI中并没有这样的视觉对象，但转念一想，这不就是折线和柱形组合图吗，应该是可以构造出来的，然后马上动手尝试，果然轻松实现，这篇文章就简单介绍一下。  

模拟个每天的数据表，以及对应的日期表，先建立两个度量值：

> 当日数据 = SUM('数据表'\[数据\])
> 
> 15日平均 =
> 
> AVERAGEX(
> 
> DATESINPERIOD('日期表'\[日期\],MIN('日期表'\[日期\]),-15,DAY),
> 
> \[当日数据\]
> 
> )

写15日平均这个度量值，主要是为了模拟两条折线的效果，关于移动平均可以参考这篇文章：[你做的预测不靠谱？是因为你不知道用移动平均！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068131&idx=1&sn=650477c6ae71dd9b6d1d31f55b37db21&chksm=8e0c75f4b97bfce2b76ac4c5e102501bae16d37701355f0f96a3f4df1a59337e1b8b858a28b6&scene=21#wechat_redirect)  

然后用上面两个度量值，放到折线和堆积柱形图的【行值】生成两条折线图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMTBmAIN2RegHGXTqiawoEfU42yJHO7AKI2soEhibJcfmQKickHFuuAdJCd77icyW81vWOXKOVTjJOF0w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下面就来看看如何在这两条折线中添加柱形图。  

**总体思路是是利用折线和堆积柱形图，折线图上面已经做好；而堆积柱形图下方的柱子是这两条折线的最小值，之间的柱子是两条折线的差额，因为还要显示不同的颜色，需要将是否高于均线分别写度量值。**

按这样的思路，写三个度量值如下：  

> 最小值 = MIN( \[当日数据\] , \[15日平均\] )
> 
> 高于均线部分 = 
> 
> IF( \[当日数据\] > \[15日平均\] , \[当日数据\]-\[15日平均\] )
> 
> 低于均线部分 = 
> 
> IF( \[当日数据\] < \[15日平均\] , \[15日平均\]-\[当日数据\] )

将三个度量值放到折线和堆积柱形图的【列值】中，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMTBmAIN2RegHGXTqiawoEfUYyXTh2AxicrV4ickicNFOxgiafKsxGndky328sRccW8HM0LUdOyaXQ992Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后设置数据颜色，将最小值设置为与背景色一致，高于均线和低于均线分别设置为两种颜色，就可以实现这样的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMTBmAIN2RegHGXTqiawoEfUfDN2c8KvJwMFT9T4wWoBUvovl5RnP1wpzfTCibX9jR9XXb3sibriaia4BQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在两条折线图中间填充折线，并以不同的颜色显示，可以醒目的看到是哪些数据高于均值、哪些数据低于均值，以及差异的大小，非常直观。  

关键是，这个可视化的制作，并没有用到复杂的DAX和操作，希望对大家有所帮助，打开PowerBI可视化制作思路。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 2k+ 学习者一起成长
