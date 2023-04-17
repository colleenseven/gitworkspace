---
create_date: 2021-04-11T20:04:41 (UTC +08:00)
tags:
aliases:
pagetitle: 推荐5个有趣的Power BI自定义控件
source: https://mp.weixin.qq.com/s/75PA-peIP6gc1dxdX9JTHQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

PowerBI提供的可视化类型非常丰富，除了内置的几十种类型，还有丰富的自定义图表库，目前PowerBI自定义视觉库中已有327个可视化对象，并且仍在不断增加中，大家可以在官网查看下载每一个视觉对象：

https://appsource.microsoft.com/zh-cn/marketplace/apps?page=1&product=power-bi-visuals

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMicFm3BIr503Psex3uc7TbWEDQo8x18odlHqcfs8RUCE1MhJFs3rUhuoZ2P2bFoDtaMOdDOwdiaWTg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中大部分是用于展现数据的各类图表，除了图表，还有一些是可视化控件。

**控件是可视化的一部分，但一般不会单独使用，它是作为图表的控制器出现的，**比如常用的切片器就是一个控件，本节介绍几个有趣的自定义控件。

这些控件以前都用过，平时很多人也问题这个是什么，怎么做出来，那么这里正好也说明一下。

___

**TextFilter**

经常有人问我报表上的搜索框是怎么做的，其实就是这个控件，比如这个报表左上角的搜索框就是用TextFilter制作的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMicFm3BIr503Psex3uc7TbWfsQ15KsPdypuIV3y16WV0CTepdazXTib8eEH9LrSqwjkialfxicAFnibFA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

使用起来非常简单，它可以对包含在总字符串中的部分文本过滤，只要包含搜索词的数据都会显示出来，与平时我们使用搜索引擎的体验类似，小巧而实用。

**Chicletsilcer**

功能强大的切片器，虽然内置切片器也很好用，但部分设置依然不够灵活，Chicletsilcer是内置切片器一个很好的补充。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxJn6Tfn6WhsYAEvhCibZic19neNeVhFia2aV8bicYge3fANfHN5vY2zJkNA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于Chicletsilcer的更详细的介绍和用法，请参考：[利用PowerBI的这个控件，美化你的切片器](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073642&idx=1&sn=d4e57071dc6421b4bb2f0bc9fc1e51b2&chksm=8e0c5e7db97bd76b1e9de73326a5676b2b5aeca519c036bbc9a30ee7a15075145783e09c55b8&scene=21#wechat_redirect)

**Time Brush Slicer**

## 十分有个性的筛选器，可以通过鼠标直接在感兴趣的时间段内选择或者拖动来过滤基于时间的数据。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMXAkiaUCXmUypetDKuVQY5k7ZF5Kv2UAaF8a0rpricSvXbNb809RbooAWZBohsuyEDibTiblH5NibuczQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

关于该控件的更详细介绍请参考：[认识一个好玩的时间切片器-Time Brush Slicer](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067758&idx=1&sn=df3248c1e5d799a72fcfbcef12c6874b&chksm=8e0c7779b97bfe6f0eaac4899b69e6b607430e3c064afc86b4d892e4ed4393bc08aeaae5dee6&scene=21#wechat_redirect)

**EnlightenWorldFlags**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMicFm3BIr503Psex3uc7TbWvCjvLzHJ2Qk2cTg6ibicZJa7cgbwKTA8YCxcx037WWgzl6q1Y0qMXb7g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个控件非常有趣，首先它就是一个切片器，不过这个切片器内置了各国的国旗图案，只需将含有国家的字段放进去，它自动显示出各个国家的国旗图案作为切片器，以一种更直观更吸引眼球的方式进行交互。

**PlayAxis**

以前的文章中多次提到过这个控件，它可以自动播放，制作动态播放的可视化必备，下面这个动态地图就是用它设计的，样式见右下角，使用时也可以隐藏：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOqXpqbp5ZUxbZBibFReOOG80ibU6ujzcBGfoficbHR5iacZLE2rlXIXF3kw7AicX6d9KHQ3pXkyYa2asg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

虽然PowerBI报告制作动态可交互报表十分方便，但一般情况下还是需要你手动点击才能动态交互的，如果你想让图表自动播放，而无需每次单击，来展示一定的进展规律，那么PlayAxis非常适合。

上面这些控件都很小巧，并且免费，设计报告时如果需要可以从AppSource中直接添加。

如果没有登录账户，也可以直接从文件导入使用，公众号后台发送“自定义控件”，即可获取上面介绍的5个控件的安装包。

___

[**新书上市**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
