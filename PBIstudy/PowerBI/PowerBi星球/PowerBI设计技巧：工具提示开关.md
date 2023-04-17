---
create_date: 2021-07-27T18:17:27 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI设计技巧：工具提示开关
source: https://mp.weixin.qq.com/s/eNpjtmSTcWakjKB_snaBuQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

[之前的文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076591&idx=1&sn=b58d43709fe14df092e63dd107c1d8cc&chksm=8e13aaf8b96423ee7bfbf3c9f9ef3643819c7f36970fb46e97bbf15fd23de54aa89380775772&scene=21#wechat_redirect)介绍了利用书签切换不同的工具提示效果，这篇文章再介绍一个技巧，在报告页面上设计一个工具提示开关，动态切换是否显示图表工具提示，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMnIRpWcONauI7mAOicBcqNhAVNqzDvL6ibAibH0cbJhIwqKowEWWIq4gNueaAJTD9O85wBicqP4oVD5Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

是不是很有趣！

工具提示能在可视化页面通过一个按钮进行开关吗？表面来看当然是没有这个功能的，那么这个效果是如何做到的呢？

其实背后的秘密非常简单，这里的树状图其实有两个，一个设置了图表工具提示，一个设置了默认的工具提示，利用书签进行动态的切换图表而已。

并且为了效果更加逼真，在报表页面添加了两个开关的图标，作为按钮来操控书签。

整体思路就是这些，如果你对书签比较熟悉，看到这里应该已经完全清楚，本文也可以结束了。

不过考虑到还有不太熟悉的同学，以上图为例，这里再简单介绍一下操作步骤。

**1\. 在原报告的基础上，复制一个树状图并分别设置工具提示**

在图表的格式面板，可以设置工具提示的类型：默认值/报表页：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMnIRpWcONauI7mAOicBcqNhtSdfr5hIicKqXLtyoShhkWTalX76kkVLxmvuqQgU45BmpEjLwy4pTicA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于这两个完全一样的树状图，工具提示类型分别设置为默认值、报表页，工具提示设置为报表页的，选择提前设计好的工具提示页。（关于如何设计工具提示页，这里不再介绍，可参考：[深入了解PowerBI的工具提示功能](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067562&idx=1&sn=c3472d97c251abf52f38e2f7e31b23a6&chksm=8e0c763db97bff2bf8d514625a3fd037d274ea3014624766b7aa2822bc63a6e2c96006223ba7&scene=21#wechat_redirect)）

设置好以后，将两个树状图上下重合叠放到一起。

当然这里也可以设置完全不显示工具提示，大家可以根据自己的需要来调整。

**2\. 插入两个图标，作为开关按钮**

准备好两个开关图标，插入进来，并上下重合叠放到一起。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMnIRpWcONauI7mAOicBcqNhtgBgQ3GSWicPvonryVS4HMIGmWYqtiabd5P9aS0GHT0oT7ibN5Wz8iacOw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于图标资源，可以从网上搜索下载，平时多积累，推荐一个好用的图标资源：阿里巴巴矢量图标库https://www.iconfont.cn/

**3\. 添加两个书签**

利用选择面板，分别设置树状图和开关按钮的显示/隐藏状态，来添加书签。  

书签的具体细节如下图所示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMnIRpWcONauI7mAOicBcqNhZntduyqgjCq45oytehX8ZniatoIh85ia636X2yaFrCgSDhM9icicEqaFtA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMnIRpWcONauI7mAOicBcqNhibooTgjlriaLqpjG6FiarjXuDn8W60xQ56Oot3o2riaLKbjMibdrVUPQicsw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**4\. 设置按钮的操作属性**

分别设置这两个按钮的操作属性，选中开的按钮，设置操作的书签为“工具提示关”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMnIRpWcONauI7mAOicBcqNhNicjZdhibJqzcUYj9EgrciaFM4JtGD3Neh9GwKh3iax55H8LLUvdpLtstQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

另一个按钮则正好相反。

至此，设计完成，点击就可以看到本文开头的动态交互效果。  

关于书签和工具提示，多动手练习，才能够在需要时灵活运用，如果对书签还不熟悉，建议看看这几篇文章：

[PowerBI中的书签，真的非常有用！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068219&idx=1&sn=b74e0d16ac61413a90fb5f7837dea112&chksm=8e0c75acb97bfcba745fe9ba7eb4ca2aa83d0af34a17668284170b97c68b2d3dc909dc9eb936&scene=21#wechat_redirect)  

[利用Power BI的按钮和书签，动态切换图表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068244&idx=1&sn=4395dc8163cded6a268dd65c3583157a&chksm=8e0c7543b97bfc5551a6626667fccb71b36b303777be57cb0339f3138d2761c43b707a01c073&scene=21#wechat_redirect)  

[报表布局技巧：折叠切片器，拯救有限的空间](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068451&idx=1&sn=5c34b75425d79e9f03cf125c0a03f110&chksm=8e0c4ab4b97bc3a2abc3822437947613babc67a03c8e324d86a9ecf947bc9f324152a3194797&scene=21#wechat_redirect)  

[Power BI报告设计技巧：动态工具提示](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076591&idx=1&sn=b58d43709fe14df092e63dd107c1d8cc&chksm=8e13aaf8b96423ee7bfbf3c9f9ef3643819c7f36970fb46e97bbf15fd23de54aa89380775772&scene=21#wechat_redirect)  

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069406&idx=1&sn=5342b16eb810a803dea5d2472441b4e1&chksm=8e0c4ec9b97bc7df8d65d5bbfeeaa95695f7d68e989179a2eeab008a49e7e2351c561a20326e&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
