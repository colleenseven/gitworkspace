---
create_date: 2022-05-28T11:40:44 (UTC +08:00)
tags: 
pagetitle: 最新发布的PPT集成PowerBI插件，你最关心的几个问题
source: https://mp.weixin.qq.com/s/xrsMCWNsvweukF_sH2i6bQ
author: 采悟
status: 未阅读
category: 
uid: 
---

很多人用PowerBI做分析报告，但是分享演示的时候希望能在PPT中进行，之前并没有太好的办法，不过微软本周终于上线了这个期待已久的功能，可以很方便的将PowerBI报告集成到PPT中。  

在PPT中嵌入PowerBI的流程和效果见下面的视频：  

嵌入的主要操作步骤如下：  

**一、PPT中找到PowerBI按钮或Power BI加载项**

现在部分PPT版本中已经多了一个PowerBI按钮：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuk6k36icICm1CrDfGRRhpkdiaGnGbAJ0UWkw1sSNjtgIVBtuXWm16LCuoe1tyJP7EGYsRhbauOcxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果没有出现这个按钮，可以尝试在Office加载项中搜索"Power BI",把它添加进来。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuk6k36icICm1CrDfGRRhpkibOmbWoxAvQLMOazkMybQeh1LaduCCDQFsdz7VYxLhSPz4ly4I09cWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是本周发布的最新官方插件，点击就会在PPT页面上显示一个输入框，可以粘贴PowerBI报告地址。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuk6k36icICm1CrDfGRRhpk66TELL2BXZlwTia21XU2AnmicOkeFIyzQg3ODK9eFdgZJbibgYUM2AzDQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**二、到PowerBI服务中复制报表地址**

进入PowerBI服务，在工作区中找到需要嵌入到PPT的报表，以下面这个报表为例：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuk6k36icICm1CrDfGRRhpkOibmpaufQeIianjGcHpjPSYwFxuBCOQ9ooH6IU4yzXQ1oicRSEeTCBgRQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

直接点击打开，然后在浏览器地址栏复制该报告的URL:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuk6k36icICm1CrDfGRRhpk9q21rgAcbAWaVrwo1mSsWDibmHGStICo5twIpuu7yVic7cpLdMjgQZ3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**三、将报表地址粘贴到PPT中**

将复制的PowerBI报告URL，粘贴到PPT页面上的输入框中，就会在PPT中看到PowerBI报告。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNM9WUJmfDibCPtmRHs6P1AI0hiaGbbth3GxMsjVUtMWCeceubU4BNoc6TicJdtRaj9FlaeZWf29lmNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以通过鼠标拖拽调整尺寸，调到页面大小就可以实现全屏演示，当然这个报告是可以动态交互的。

上面这几个步骤非常简单，不过很多人尝试后发现并不能成功，这里就将大家关心的问题统一解答如下：

**1\. 什么版本的Office可以使用？**

因为刚发布，只有个别版本有此功能，我测试365商业版可以做到，365国内个人版好像还不行。

**不管是什么版本，只要你能够在PPT功能区中看到Power BI按钮、或者尝试在 Office 加载项搜索，如果能找到Power BI加载项就可以使用。**

如果你的版本里找不到这个按钮或者加载项，就是还不支持，再等一段时间，或者尽早升级到365，新功能肯定是365最先用到的。

**2\. PowerBI报表需要发布到web吗？**

不需要，这是新的插件和之前用的Web Viewer最大的区别。

**因为不用发布到公共web，只需要工作区中的报表地址就可以嵌入，数据的安全性就有保证，不用担心数据泄露风险了。**

事实上新的插件也只支持报表的URL，不支持发布到web的URL，如果你复制粘贴的是web的URL,它会提示URL无效。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuk6k36icICm1CrDfGRRhpkkY0BS0ftyhhCic2DUored1SpZQiafiabKYl4dljN7wMZiaXuAlF8TdriaWg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果你想用发布到web的网址，依然可以用之前介绍的Web Viewer插件：

[如何在PPT中动态交互PowerBI报告？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068966&idx=1&sn=4a1d6126f98501f4f830f4a78f947022&chksm=8e0c48b1b97bc1a70c931eab032724a24f2a13ea686cae7bc7a934376a9103e504975c0138c2&scene=21#wechat_redirect)  

**3\. 发布到国内PowerBI服务上的报告是否可以？**

目前还不行。

国内世纪互联运营的PowerBI服务，复制工作区中的报告URL，粘贴到PPT中无法使用，网址粘贴进去会报错：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOuk6k36icICm1CrDfGRRhpkDe1xldeX6xKMOVK6lhpFrZEGxch1VHjtw7a6nTHFGicfXCOfKnzIdFw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不过既然国际版可以使用了，国内的应该也快了，耐心再等一段时间。  

**4\. 是否必须拥有PowerBI Pro许可证？**

不是必须Pro，免费的PowerBI账户也可以使用该功能。

在PPT中，在不注销原账户的情况下，点击使用其他账户登录，然后用你的PowerBI账户登录（可以是免费账户），登录以后，加载PowerBI插件，然后将该账户中的PowerBI报告地址复制到里面就可以查看了。

**所以，关键还是Office版本，只要Office版本中有PowerBI加载项，任何PowerBI账户生成的报告都可以集成进来。**

**5\. PPT分享给别人还能打开吗？**

取决于对方的权限，如果对方有权查看PowerBI工作区中的这个报告，那么他就可以在PPT中查看报告，反之就不能。  

**也就是说PPT嵌入的报告，仍要遵循PowerBI本身的权限控制，而不能突破这个限制，否则谁都能打开，PowerBI报表的安全性就丧失了。**

因此这个新的插件主要是利用PPT强大的演示功能和庞大的用户群体，来讲述PowerBI报告的故事，而不是用PPT文件传阅分享PowerBI。

**6\. 其他问题**

还有不少人关心的问题是：不登录Office账户可以用这个功能吗？不联网可以用吗？WPS可以用吗？

答案都是：不可以。

___

以上是根据目前版本测试的结果，如有不准确/不完整的地方欢迎留言指正、补充，随着版本的迭代也许会有不同，期待越来越好用的Power BI。

如果你还有其他问题也可以留言交流哦~

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
