---
create_date: 2021-05-29T19:57:24 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI账户登录提示安全默认值？通过这个设置轻松关闭
source: https://mp.weixin.qq.com/s/h70BUwzSosKyJicNv5zrzA
author: 瓶子
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

> 文/瓶子
> 
> PowerBI星球嘉宾，目前从事职考行业的数据运营，喜欢钻研power bi和excel来实现自动化

之前PowerBI星球发过一篇如何获取Power BI超级账户的文章，链接如下：

[超级秘籍：免费拥有可发布的Power BI账户](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070700&idx=1&sn=7b97e421ea46cbfacca3f6aed4ef1720&chksm=8e0c43fbb97bcaed90c9d5b835de96be15e16e7944c5cf075a98232b41b3236f3ab95dd38d20&scene=21#wechat_redirect)  

很多人利用这种方法注册了自己的账户，但是星球会员群里不少人提到，通过这个方法注册的新账户或者以前注册的账户，最近在登录Power BI服务时会提示安全默认值，如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPtXI4ySS3TjtL24lhzJNwvUcBcZm14DicG3XRcyoplgLLeJu4ltiaMib0w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击下一步，显示需要下载安装Authenticator这个应用，每次登录时利用这个应用来验证身份，如图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP8ZdKkYib3qicQPWaLHyhAQiavCpm4vDcBjIhZfA6RfNPEny3vAYmQib30Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这是微软为了保护全局管理员的隐私安全特意设置的一个方案，如果想提升安全性，可以点击“立即下载”安装这个App，如果下载遇到问题，可以在公众号后台回复“**Authenticator**”获取这个应用的安装包。

当然如果你不想下载安装，也有解决的办法，下面的设置可以帮你轻松取消这个提示。

第一步：使用邮箱登录已经注册的Azure账户，网址为：

https://portal.azure.com

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOhzich2Ujr0FFTlCwUmeExWZLicteDUDffeRbpdp2GHbnDCoCicic3udribReWBZGLyjzJkMhZqZdjoLg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第二步：登录Azure官网后，点击Azure ActiveDirectory的查看选项。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjP0jQ8wNMO6XVglEHTqvZfeqibBUJYg4kddwDf5Pczqafp4LlPNDVUaOg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第三步：点击左侧下方的属性按钮，然后再点击右侧最下方的管理安全默认值。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPhkPRsNiaDry1IGbsiaMrfibaheibra2Ertdibez5ibeyabDWibJZK4h9hN1Nw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

第四步：第三步点击管理安全默认值后，在右侧出现一个启用安全默认值编辑框，启用安全默认值选择否，原因任选一个，最后点击保存。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMAOGgCF1hLCCOtIoVy4GjPRWOM9nLnGG0matRlfcHjCc5KdQNzvW5TOYLmxTmABKxIWIJrFVkiaiaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过上面的操作之后，再登录你的账户就不会有启用安全默认值的提示，直接输入账户和密码就能登录了。

如果你下次登录遇到了这个问题，就用上面的方法解决吧。

___

**[新书上市](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

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
