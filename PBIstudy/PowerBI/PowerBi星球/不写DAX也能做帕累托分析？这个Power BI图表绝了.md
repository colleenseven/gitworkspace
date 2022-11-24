---
ZK: Origin
create_date: 2021-10-31T12:57:43 (UTC +08:00)
tags: 
aliases: null
pagetitle: 不写DAX也能做帕累托分析？这个Power BI图表绝了
source: https://mp.weixin.qq.com/s/eeJAFrEQ9R9vCxNIg4AWaA
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

帕累托分析很常用，我们之前也多次介绍过帕累托图的做法，包括静态、动态以及特殊数据的处理：

[使用PowerBI制作帕累托图](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067854&idx=1&sn=bd282fa65514734b6762b63704fae8f2&chksm=8e0c74d9b97bfdcf7677fadf031b177fd1e89b8a5695928f8e33173cb6a338d03d221ebb7953&scene=21#wechat_redirect)  

[用PowerBI进行帕累托分析有多简单？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067876&idx=1&sn=ba8ad9deb639090dcf087dceb95c8131&chksm=8e0c74f3b97bfde5d8908228131977bf957e6792e3ebce4ee5eefe43dee483ce6c597151b4ab&scene=21#wechat_redirect)  

[Power BI帕累托分析：数值相等时累计占比计算“错误”问题](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071565&idx=1&sn=3fe93535f6408a76264d0841eae77746&chksm=8e0c465ab97bcf4c8faf4d7bb6d1a4c252a5cb755fe2ee7f42c6213744f2be62de352fbd9993&scene=21#wechat_redirect)  

无论是哪种做法，为了完成帕累托分析，都需要利用DAX写度量值，来计算累计占比，并使用折线和柱形组合图来实现。

其实在自定义图表中，有个图表可以自动生成帕累托图，它就是Pareto by sio2Graphs，你可以在AppSource中直接获取。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtS3libZib4ozSv2u2nBMZaRoTxAI9XezSaBjotd3GpFNN35d37FVYE8Xxu79Z7odNzONx2icc8VEOw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个图表的使用十分简单，只需要两个字段，直接拖拽到类别和数据框中，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtS3libZib4ozSv2u2nBMZaR3esEpy1SWLwqLFxSdp76ljjISmyLg4Fp63GtYZwpgUDwZxRib0mDdIg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就会生成一个帕累托图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtS3libZib4ozSv2u2nBMZaRWMlUFsUKmsa6UB1k7zdkYMQ0QBw7UNOY33IfXt7yibS50D9vZ1fu7dA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常简单。  

之前我们可是必须用DAX写度量值才能实现，并且累计占比度量值也不是初学者随便学习一下就会写的，即使模仿着写出来也未必能理解，还是需要一定的基础才能真正掌握的。

而**这个自定义图表，内置帕累托的计算逻辑，自动对数据排序并计算累计占比，并直接用柱形展现出每个类别的数据，以及累计占比的折线（非常平滑），无代码实现帕累托分析。**

它的格式设置也非常简洁，简洁到可自定义调整的元素非常少，主要是字体和颜色格式的调整，

比如在类别中，可以将柱形颜色调整为渐变，折线的颜色也可以调整，上面的帕累托可以轻松设置成下面这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtS3libZib4ozSv2u2nBMZaRCLRRqzUPknw6O6Wicw2ibNUSen53zjiaxS487oSmK64gKvlF4LB69AN3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不过**这个图表目前最大的硬伤是，x轴只能显示10个类别**，超过10个，它会自动取最大的前10个来计算，其余的默认忽略了，也许它的初衷是遵循帕累托的内涵，只关注最重要的类别。

所以如果你的数据类别较多，就不适合用这个图来展现，还是老老实实按照帕累托的计算逻辑写度量值来实现吧。

无论如何，这个图表提供了一种可能性，在较少类别的情况下，允许用户以拖拽的方式轻松完成帕累托图分析，也希望后续的版本中，该图表能够突破类别的限制。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYCTV9SBx5LXD4kp3icA9LouW3YN2z2njBWWQzM1zia9Fbeky0fdIpNakw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和3900+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCy5RUEz1Yp2hsG1ExlG3XiaqfWPqspJ1oiaEcKjuJCKPStBaWQXO6SOew/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
