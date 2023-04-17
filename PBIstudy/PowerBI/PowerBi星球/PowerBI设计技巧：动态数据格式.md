---
create_date: 2020-12-23T23:42:42 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI设计技巧：动态数据格式
source: https://mp.weixin.qq.com/s/rIX64xEeITEJiWXcFUnUZQ
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

之前分享过一篇[动态指标分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067957&idx=1&sn=93e3f3b54fd902e26ce98f8c4112abbb&chksm=8e0c74a2b97bfdb405f86c58998f8320ea8c26853b039edfd2c7f6d8cef0d97d28dacfe9d23f&scene=21#wechat_redirect)的文章，利用这种方式，可以轻松实现在一个图表中多个指标的动态分析，但是这种方法有个不足之处，也是让很多朋友困扰的地方，就是各种指标的数据格式没法自定义调整。

比如对收入、利润和利润率这三个指标进行动态的展示，先写好这三个基础度量值，然后利用一个度量值，将这三个基础度量值整合为一个度量值：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOGMSYGohYe2pjHphY6PIuJ93Z0ibReymJlvC0blnd4slc7iciadg1aE1PAydnCOicvicRussLNWqDx7oA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后利用这个度量值就可以进行动态的指标分析：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOGMSYGohYe2pjHphY6PIuJYFfDwiaF4Wh4tlWNO8m3uepTkSMBicDV7ARW3c2icDXkcf0eia5Xib7iaAHw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

详细做法参考：[PowerBI作图技巧：创建度量值进行动态指标分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067957&idx=1&sn=93e3f3b54fd902e26ce98f8c4112abbb&chksm=8e0c74a2b97bfdb405f86c58998f8320ea8c26853b039edfd2c7f6d8cef0d97d28dacfe9d23f&scene=21#wechat_redirect)

通过上图可以看出，所有的数据都是保留两位小数，如果想让利润率单独显示为百分比格式，是无法做到的，因为一个度量值只能设置一种格式，这三个指标只能同时显示为千分位、或者百分比格式，这显然不能满足我们的要求。  

在前面提到的那篇文章发出的时候，还是2018年，当时是无法实现各种指标分别自定义格式的，不过现在可以利用今年发布的计算组来解决这个问题。  

关于计算组的介绍和使用方法请参考这篇文章：[PowerBI发布重磅更新，一文带你熟悉计算组怎么用](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072054&idx=1&sn=d403fdef264cbfb6fca46d33bd0083b9&chksm=8e0c44a1b97bcdb7fe466afe90d0f3d4b86738a0da7241f9125d4f36a1fcbd89c094b7ea42d8&scene=21#wechat_redirect)

利用计算组，我们想要实现的效果是，**让收入和利润指标显示为千分位格式，并带上货币符号￥，而让利润率显示为带两位小数的百分比格式。**

下面进入操作步骤。

**1、在外部工具中打开Tabular Editor，并建立计算组，可以命名为动态指标分析。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOGMSYGohYe2pjHphY6PIuJngAH5UKxOdxYqqcccAibRsFv8icSsQrMSJ3aXUFabzAVXpeZWd8Ad5gQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2、按照分析的指标新建计算项，并设置格式。**

收入计算项可以这样设置：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOGMSYGohYe2pjHphY6PIuJHuZ9YPr6hD6Ov9ibwJX92szDlKPkicqMLzYH6HWqPJ995YvvDFHjQFPA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其表达式可以直接引用已经建好的基础度量值\[收入\]，并设置其格式为"￥#,##"。

同样的方式建立利润和利润率的计算项。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOGMSYGohYe2pjHphY6PIuJicbZiaSPu79K3tkd5sQhJSBr5l1N4ibOiaKXX497IpNdria0g9HF5wDX7Ug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOGMSYGohYe2pjHphY6PIuJfvbBv5flicpEYU722VaW13pxia29Tbp6VzCY2bVaHia0nCWcZle8EnD4A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

保存后，关闭Tabular editor窗口。

**3、利用计算项生成切片器，并用任意度量值生成一个图表，就可以实现动态的指标以及动态的格式了。**

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOGMSYGohYe2pjHphY6PIuJialI0MNyiadS6Er3tFugAo3ITicOl76Pcf2XG3lvAgCV7iaDCFts8ibWia9A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

各种指标的数据格式正是我们需要的。

利用计算组可以轻松实现动态指标的动态格式，虽然不复杂但略显繁琐，还需要跳出到Tabular editor环境来设置，不够简洁直接，希望PowerBI自身能早日实现这个功能。  

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 2k+ 学习者一起成长
