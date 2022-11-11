---
aliases: null
create_date: 2022-01-07T12:32:37 (UTC +08:00)
tags: 
pagetitle: 利用PowerBI这个自定义对象，轻松展示列表信息
source: https://mp.weixin.qq.com/s/0hVre_Mub0FgBqDlWCfRDA
author: 采悟
status: 未阅读
category: 
uid: 
---

Power BI展示列表信息，一般会用内置的表格或者多行卡，今天分享一个自定义可视化对象，相对来说可以实现更美观更丰富的展示效果，它就是Overview by CloudScope。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNQV3ahE0AoxbSHRaXl8oQGSqOBjRgKKHCHQLAQ1QdBOzX7n3B4ruPm3r0sQ6RZ8XZFBFJ0tCTrgA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个图表设计的初衷用Instagram的样式来展示社交平台账户的主要信息，比如展示某个平台上每个用户的粉丝数量、关注数量和发帖量：  

不仅以文字的形式展示，还可以同时展示图片，以及可以点击的链接。

虽然是以Instagram的样式展示，但数据并不是必须只能来自Instagram，也并不是只能展示网络平台账户的信息，我们同样可以用这个图表来展示其他类型的列表信息。  

比如之前介绍过[如何利用PowerBI获取豆瓣读书TOP250](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070458&idx=1&sn=c4c2f4de681ef66524b91209e83dd769&chksm=8e0c42edb97bcbfb525a923d9d7378095f91ae9e3d592e28b7918ee1ea8a991b49ed4017fee0&scene=21#wechat_redirect)的信息，有了这些信息之后，不仅可以用表格来展示，也可以用今天介绍的这个图表，这里就以这个数据为例简单介绍一下该图表的用法。  

该图表只有一个字段框，将表中需要展示的每个字段直接拖拽到里面：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNQV3ahE0AoxbSHRaXl8oQG23qVkibhL9tNCqQRHvich1WhLXS69dQfm4C3c7W4ECYj0gegVPJmE4mQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后可能并不能显示出来信息，因为还需要在格式设置中指定每个字段的映射类型，比如我这样设置每个字段的类型：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNQV3ahE0AoxbSHRaXl8oQGiazRs6qhVGVpe9ghHKIPVm84VzIzbyeTicx29YSvwr7YCIqo0s6lQ7YA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并设置细节格式：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNQV3ahE0AoxbSHRaXl8oQGQSZJliaI3bkNJ5XLicphMXSTcEeiccbLCoicHgQC5HZuKpMvl47910T7Mw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个图表也只有这两项设置，非常简陋，但效果还是可以的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNQV3ahE0AoxbSHRaXl8oQGhHkRxN9iaYF24yNsg903hMWYnaXsobcXYYZMqASq1zudMZh2HIYxYgg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

它可以显示图像以及跳转网址，前提当然是需要你的源数据中有这些信息，并在PowerBI中设置图片字段的属性是“图像 URL”，网址的属性为“Web URL”，它才能正常显示和跳转。  

当你的报告中需要展示类似的列表信息时，可以尝试使用该图表。  

[**PowerBI星球的最新版****内容合辑****，值得你收藏学习：**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN8YOicNXzCaSLpQrKXOL0LsNeYw0fj3iaGFy7XSwwmibHicdtiaHEbhgmHSPXQlkg3WiaVA4hJ8PGDcdEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
