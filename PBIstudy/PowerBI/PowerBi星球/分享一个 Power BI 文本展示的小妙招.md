---
create_date: 2021-02-03T20:18:06 (UTC +08:00)
tags:
aliases:
pagetitle: 分享一个 Power BI 文本展示的小妙招
source: https://mp.weixin.qq.com/s/0JEMwDjn_4RL478Gqb7qUA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074639&idx=1&sn=03b003d199f754794c0bac8af15c50e0&chksm=8e0c5258b97bdb4e0aa92667a047bca5c7705f86a6c2b4ac66e3eefc171ca95e6891a433ecff&scene=21#wechat_redirect)关于如何用度量值显示表的文章中，有一个方法是将列表连接成一个字符串，并用卡片图显示出来，就像这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPoT4k4an0MEQe427woeQyeIhic7szGtc8VonlZ0DSfTVuRdIHoH0JHcEfl958g9uoNbLPnfiaSSqQg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这个卡片图看起来好像并没有什么特别的，但是细心的朋友动手一做，发现自己做的卡片图是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOojexubCy39PJZJic24XlI9QE5BtbJvG1Kev7xJ7NSL3Wd29P5WgOgsbm93Q9bhGicjp0UwEmOEPYw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

无论在卡片图的格式面板中怎么调整，也无法实现自动换行、左对齐的效果，那么最上面那个卡片图是怎么做到的呢？

如果看到这个卡片图所用的度量值，你也许感到更加惊讶：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOojexubCy39PJZJic24XlI92aLnw2HhfMDDTJG3iccTFSuxSyo47TiaECEsEPbnNhcQJ2zxUbUxgt0w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

共同客户的度量值是这样的：  

> 共同客户 = ""

是不是很诡异，一个空的度量值是如何显示出这些文本的呢？  

最初还是星友拿一个源文件问我的问题，刚开始看到这种卡片图也觉得好奇怪，不过很快就想到了原因，其实这些文本是卡片图的动态标题。

将我们需要展示的文本度量值不要直接放到卡片图的字段中，而是打开卡片图的标题，点击fx，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOojexubCy39PJZJic24XlI9FUvkQfea95FaXFczlRBQ81Db8E3kicvGVibsiczpqhp98yFzkoJIov4og/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后选择度量值即可实现：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOojexubCy39PJZJic24XlI9rPMjur0L3WOc7wsOLuxiaOGe1eQCHTptEH3cWDl764MWcnMficeU1oRg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**通过标题，文本内容不仅可以像正常的卡片图一样动态的交互，并且还可以调整文本的对齐方式、是否自动换行等，比卡片图的数据标签设置更加丰富。**

当然为了让卡片图能够正常显示，还是需要放一个字段进来的，所以就用了空度量值""来占个位置。

如果理解了这个原理，完全不用局限于卡片图，任意一个图表，只要标题支持条件格式，都可以实现这种效果，比如饼图的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOojexubCy39PJZJic24XlI9ibISwtSBREMSicY4lCWCYzfXRumbFiadtiaHCjNXfDVI3zHJBiczxpM6I5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不得不说，这种方法很巧妙，也很隐蔽，当你觉得卡片图的数据格式不能满足需要时，你也可以尝试一下这种玩法。

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
