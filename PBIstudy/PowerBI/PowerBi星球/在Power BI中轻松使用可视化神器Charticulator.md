---
create_date: 2021-04-22T20:02:44 (UTC +08:00)
tags:
aliases:
pagetitle: 在Power BI中轻松使用可视化神器Charticulator
source: https://mp.weixin.qq.com/s/pr_zPgoCvaEBYj-WY1k0fQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

Charticulator是微软研究院发起的一个免费开源的可视化项目，它让用户无需编写任何代码，便可设计出各种惊艳并且可复用的可视化图表，之前只能在官网中制作，虽然支持导出后PowerBI自定义图表，但用起来比较麻烦，并且也不稳定。

PowerBI desktop2021年4月更新后，把Charticulator集成到了自定义图表库中，在AppSource中即可直接添加。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3aia4JD0VbYCfl7B9fVbqzGibkzZLOtKxg1JVJFwzqjzAaXhdjicf3qaGw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

利用它，在PowerBI里面就可以设计惊艳的图表，这样用起来就方便多了。  

**虽然不用编写代码，但并不代表任何人上手就能使用，它的操作界面、以及可视化设计逻辑并不简单，不花费一些时间摸索，是不可能做出像样的可视化效果的。**

所幸的是，Charticulator官网还提供了一些现成的模板，我们只要将这些模板导入，就可以生成对应的可视化图表了。

目前有13个模板可以使用，可以在这里下载：

https://charticulator.com/templates.html

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3ZMejkTITOL2TRNqYlnPuImkMxSHxtCTa4koQRhUJohdcdMic5OMjZ9A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果不方便下载，也可以公众号后台发送"**Charticulator模板**"获取这些模板文件。

以这个简单的孔雀图（Peacock Chart）为例，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3zvD5jmibfYS6L0I5OqG5giafk9BiaIfbxo5PWnFUsVm136Z6mia0ic7zoog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

来看看如何在PowerBI中快速应用Charticulator模板来制作精美的可视化图表。

**1、加载Charticulator并在画布中添加该视觉对象**

画布上添加后，它会自动显示作图步骤：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3JTvpYibT4MGGXPMwBxfEic19WPwhsEBxwFogiaic5ZALTXAibRBNicJsf5og/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2、在字段区添加数据字段**

假如我们想用孔雀图展示每月的收入数据，可以将这两个字段放到【data】中：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3csqG4eh1SYQPKhgwjVP4KkPNjfXqnlaGic2hJ3uibvib42JWAasg45UqQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3、点击右上角三个点，选择"编辑"**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3rM2QKaUsIRDcg7DdHrEQaY5jrZLk78JgOIfve2ajm2WeiamKhDjLdJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**4、导入模板**

在弹出的窗口中，选择"Import template",导入提前下载好的模板，模板文件的后缀是.tmplt

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3ZOEZDHptt5Z4bib1ehOKGn8pmyxgQsrXUK35SS9JaO8tMCHxd6NicFDg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

左侧的按钮是进入操作界面设计报表，如果你已经会用了，不需要模板，或者要学习如何操作，也可以点击这个按钮。

**5、选择数据字段**

它会自动识别之前我们拖进来的字段，这里只需要一个数据字段\[收入\]，直接选择并点击保存即可。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW37yH9bY9RXs0BSsE59LdsbzRbGn0yYs7zd4fSNUAUiaU78iavI41MPgNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就看到了Charticulator的操作界面和这个已经根据模板设计好的图表：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3pnt7IoAJvIUM4sRWkE2LcctnxTEaZlr3KVroYHymJ4UO7Zia5c1Z24g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**6、编辑图表**

在这个设计界面可以对可视化的各种元素进行修改，刚开始用，不会操作的情况下，这里也没有什么可编辑的，不过图表标题需要修改，可以双击直接修改：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3nMib8d8HAFxmdK14Q4LW4EWKaGJLNTnCf6dD5ATfSS08tBjrOochoJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**7，保存并返回到报表**

点击设计界面左上角的"Save",然后再点击"返回到报表",这个可视化就制作好了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3rziaydHkpQjiaqHt7YdOpWRV9UcicibeQ20seksJN3MQ2HKGrk8Z3Gdicvw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

利用Charticulator模板设计的图表也是可以动态交互的：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3SxbJLDs0dJdUrWmHLov3Yrs1NwHy2v4JEHtDI838xjJGSe9icT6iahIw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

以上就是在PowerBI中利用Charticulator模板作图的步骤，其他模板的用法也类似，还有这些精美图表的模板等着你去用哦：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3mooHr5mpK8C5I671OJImX6mBIGU8Peblj7Aass8gJc6b60Jd8MVpcA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3RicaBVyCAUgB6aibjzwJbiaRJHjVoYU96OVSgFQHLqibnpNb1XBHiaNBQlw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO8GAHpgn2VqcsthVCrMibW3o5Xhts6GynIFXsz8so23QJEZyImJrhvXrLNs1sbYgnYarryYgib8tEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常炫酷。

如果你想深入的学习Charticulator的用法，可以在官网中观看这些图表设计的操作视频：  

https://charticulator.com/docs/video-tutorials.html

先熟悉界面、模仿操作，领会其中各种设计元素的用法，多练习，然后才能利用它为自己的报表效果带来更多的设计可能性。

___

[**新书上市**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
