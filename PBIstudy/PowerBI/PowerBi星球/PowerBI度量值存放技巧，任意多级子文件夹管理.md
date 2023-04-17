---
create_date: 2021-04-17T20:03:32 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI度量值存放技巧，任意多级子文件夹管理
source: https://mp.weixin.qq.com/s/Ixi752Ab8l5bXUfdRfjCJQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

今天周末，分享一个度量值管理的小技巧。

如果你做的Power BI报表比较复杂，创建的度量值很多，有必要将他们放到一个表中，并分组管理，关于度量值的管理方法，以前分享过一篇文章：[利用这3个步骤，轻松管理你的度量值](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069973&idx=1&sn=b14786fae234c7da3055c38f641d8556&chksm=8e0c4c82b97bc594eb16dd48bdf2c8b853f741b3a29cb6d9eee7881fcd0fd114d1b4515adfe0&scene=21#wechat_redirect)

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJONFAu8lNLsRCrdnBFgLkNDHlib2v706OgTib2tSyGLZURia57SZM52ehxcTYeibMwawyJO7S5e9ycYMQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

做到这一步后，还有人问，如果度量值特别多，想更进一步的细分管理，能不能在文件夹下面，再继续创建子文件夹呢？

这里就来分享一个创建子文件夹的小技巧。

依然用上图中的度量值的例子，如果想创建子文件夹，可以在模型视图下，选中需要放入子文件夹管理的度量值，然后在文件夹名称框中，在一级文件夹名称的后面加上“\\子文件夹名称”，就可以在原文件夹下面自动创建子文件夹，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPysZ7bQny1423Js6Gnt6rOTtFU6z9SGO1DWdIRFl31CeEjicAv8Xs6GkibicBSAsl0x8oKewicjFx7NQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

当然不止是创建一个下级子文件夹，利用这个方法，我们可以一次性创建任意多个层级的子文件夹：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPysZ7bQny1423Js6Gnt6rOvrAh2Puxic5LcERvTRrYMTcIHEBqsQhl2gia0DWmb7ZgVHCibXHzWc0Bg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

是不是非常方便。

文件夹建好以后，其他度量值同样可以拖动到任意一个、任意一级的文件夹中，更方便我们对度量值分门别类的管理。  

这个技巧，你学会了吗？

如果你还不知道如何将度量值放到一个表中，还是先看看之前的这篇文章吧：

[利用这3个步骤，轻松管理你的度量值](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069973&idx=1&sn=b14786fae234c7da3055c38f641d8556&chksm=8e0c4c82b97bc594eb16dd48bdf2c8b853f741b3a29cb6d9eee7881fcd0fd114d1b4515adfe0&scene=21#wechat_redirect)  

___

[**新书上市**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
