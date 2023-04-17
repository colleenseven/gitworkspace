---
create_date: 2021-07-13T19:42:37 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI报告设计技巧：动态工具提示
source: https://mp.weixin.qq.com/s/M9Rng6LHZ78_Y1tLcfd3ug
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

之前的文章中介绍了PowerBI工具提示的用法，通过鼠标悬停，弹出一个迷你的图表展示详细信息。  

昨天在会员微信群中，碰到有同学问，能不能设计几种工具提示，根据不同的按钮切换，让鼠标悬停后弹出的迷你报表动态显示不同的效果？

其实这种效果可以利用工具提示和书签，将二者结合起来，是很容易做到的，就像下面这个报告的交互效果，

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO9gjBCKz2sSd5RY408697tGBcWtM9qIcDCDhKcH7yWPAGuIOVLXl0AAXZmV3PZYIdjGpKEZCU4pw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

下面就简单介绍一下这种效果的设计思路。

**1\. 建立一个工具提示页面。**

关于制作工具提示页面的具体步骤，请参考：[深入了解PowerBI的工具提示功能](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067562&idx=1&sn=c3472d97c251abf52f38e2f7e31b23a6&chksm=8e0c763db97bff2bf8d514625a3fd037d274ea3014624766b7aa2822bc63a6e2c96006223ba7&scene=21#wechat_redirect)，这里不再详细介绍。

**2\. 在工具提示页面设计两种可视化类型。**

根据需要在这个工具提示页面设计不同的报表内容，比如这个示例中，让工具提示动态显示数据或者图表，就可以分别建立一个矩阵和一个组合图，并叠放到一起，以便于动态的切换。

**3\. 在工具提示页面建立两个书签。**

利用“选择”面板，分别设置两种可视化类型的显示/隐藏状态，并建立两个书签，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9gjBCKz2sSd5RY408697tpCMPvaiaOlx2IWwthZQMuaQWHIzHOVvaxnRVdsQEQiaHBcOsIvCs7RDA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

具体操作步骤也可以参考：[利用Power BI的按钮和书签，动态切换图表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068244&idx=1&sn=4395dc8163cded6a268dd65c3583157a&chksm=8e0c7543b97bfc5551a6626667fccb71b36b303777be57cb0339f3138d2761c43b707a01c073&scene=21#wechat_redirect)

右键上面建立的两个书签，设置书签的属性，将“当前页”勾选去掉：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9gjBCKz2sSd5RY408697todYS7amRZtViaWEykLcRpWDibINH68icBzWdTicG3LyVX40neIia0h4YGTg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个设置非常重要，去掉这个属性以后，可以只切换该页面的数据，而不需要跳转到该页面。

**4\. 制作按钮来切换工具提示效果。**

在报告页添加两个按钮，操作属性分别设置为上面设置好的书签，就能实现点击按钮后，动态切换工具提示的效果。  

上面介绍的是两种工具提示的切换效果，如果需要更多的工具提示类型，也可以按照同样的思路来制作。

只要理解了PowerBI中书签和工具提示的交互逻辑，可以设计出很多个性化的交互效果，如果你还是不太清楚，请先学习这些基础功能的用法：

[深入了解PowerBI的工具提示功能](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067562&idx=1&sn=c3472d97c251abf52f38e2f7e31b23a6&chksm=8e0c763db97bff2bf8d514625a3fd037d274ea3014624766b7aa2822bc63a6e2c96006223ba7&scene=21#wechat_redirect)  

[PowerBI中的书签，真的非常有用！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068219&idx=1&sn=b74e0d16ac61413a90fb5f7837dea112&chksm=8e0c75acb97bfcba745fe9ba7eb4ca2aa83d0af34a17668284170b97c68b2d3dc909dc9eb936&scene=21#wechat_redirect)  

[利用Power BI的按钮和书签，动态切换图表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068244&idx=1&sn=4395dc8163cded6a268dd65c3583157a&chksm=8e0c7543b97bfc5551a6626667fccb71b36b303777be57cb0339f3138d2761c43b707a01c073&scene=21#wechat_redirect)  

___

**[新书上市：PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
