---
create_date: 2021-01-04T20:22:55 (UTC +08:00)
tags:
aliases:
pagetitle: 如何为Power BI报表设计动画背景？
source: https://mp.weixin.qq.com/s/dzwPT8UBgyRDn3p9yQJ8oA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

PowerBI制作可视化报表时，默认的也是最常用的就是一张白色背景的画布，但PowerBI报表并不总是如此单调，我们还可以设计得更加个性一些。

在PowerBI中，报表的背景是通过格式面板的"页面背景"或者“壁纸”来设计的，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMLJ0JBoPy79SOjibOP2vicn0JicIicXwAIYZBAXibEWSp1scVJStmpoYdfLSsNEvpYCBOPkcVugxicTxWA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

二者的设置元素一样，比如页面背景可以调整的格式如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMLJ0JBoPy79SOjibOP2vicn0nO9r3OMqPwy1LwjXOxpbpR2ibDKrUjT4FRyB3PTGDsJaiaSq5pmlBjQg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以设置画布的背景颜色以及透明度，还可以插入一张图片作为背景，在财务报表分析案例中，首页的背景就是一张图片：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMLJ0JBoPy79SOjibOP2vicn0dgWptnbCqYHBCmZK7BYp3Wia4sMXKbftTZq2BuNR6jLiaY1aDv7WFH2g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

也可以将图片插入到壁纸里，壁纸设置与页面背景完全一致，只是壁纸不仅显示在报表区，还可以显示到报表尺寸以外的区域，所以设置壁纸，同样可以作为报表的背景。

既然用图片可以作为报表的背景，那能不能用动画作为背景呢？比如很多人问过我这个是如何实现的：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMLJ0JBoPy79SOjibOP2vicn04d1V24LfwJahibCj7IMFiccl0oN7K9Ly3LqFeyZxJVROCSfGIPPPrAIQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

其实原理就是上面介绍的背景插入图片，不过这个图片不是静态的，而是gif格式的动图。（上图中同时设置了壁纸，静态图片的壁纸+动态图片的页面背景）

**如果你需要在报表中设计动态的背景，提前准备好你要使用的gif格式图片，然后页面背景或者壁纸中选择这个gif图片的本地保存路径即可。**  

是不是非常简单，分享几个动画背景的报表效果，

这样的报表看起来更有设计感一些，你也可以尝试一下，不过尽量不要用太大的gif图片，否则对报表的打开速度可能会有影响。

___

**PowerBI星球的**[**历史精华文章合辑**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)**，值得你看一下：**  

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNn5eia186067w5or6WoVmwdm210CYQfaibhdzFvJvR59sFUgk13iauEzR4oLzGvXiaziaX8VJcB2sCbzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

___

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和 2k+ 学习者一起成长
