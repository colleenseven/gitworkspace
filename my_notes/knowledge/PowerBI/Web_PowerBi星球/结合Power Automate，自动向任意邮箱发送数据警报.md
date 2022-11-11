---
aliases: null
create_date: 2022-03-01T12:20:43 (UTC +08:00)
tags: 
pagetitle: 结合Power Automate，自动向任意邮箱发送数据警报
source: https://mp.weixin.qq.com/s/PcXa4MaoGwy7GzaXQZB5IQ
author: 采悟
status: 未阅读
category: 
uid: 
---

[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079277&idx=1&sn=b2b99267df32b25d6bc79dac3917b4a9&chksm=8e13a07ab964296cf449b073139e7c09635c659c24f0327a03098a67c71d046b657c9948081e&scene=21#wechat_redirect)介绍了如何使用PowerBI中的数据警报，其实它不仅在PowerBI的通知中心发出消息提醒，还可以结合Power Automate将提醒通过邮件的方式，发送给任意的其他用户，这也是Power Automate协同PowerBI的一个经典应用场景。

下面接着来介绍如何实现数据警报的邮件通知。  

在管理警报的设置面板，最下方其实还有一个链接：

**使用 Microsoft Power Automate 触发其他操作**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPaNYiciarZZBBZNdXTJOKfA7edF2j3Vic6mLYdlYolpaY3fO5Iw8ibBwVic4odzhuBZib8Fzo834Kke2KQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

点击这个链接，就可以进入Power Automate界面，并自动发起一个流:

使用Power BI 数据驱动警报触发流

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPaNYiciarZZBBZNdXTJOKfA7HIVeIK8BWhJd5SsrJbVqfSXTLGwiagPr5JysibUT6Ten8AXnfxb0HXHw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

点击继续，选择之前已经建好的警报：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPaNYiciarZZBBZNdXTJOKfA7lrNXOQmib7ZdKia6I594PqrXUNGIo8ZGFAA0hocUZItkofW5iaaia9FwIQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

添加新步骤，搜索“电子邮件”，选中并进入操作“发送电子邮件（V2）”，  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPaNYiciarZZBBZNdXTJOKfA7kFH3UqFe2FvrbXbYQm4TlxPMaBoBubLzbibcYympFv5O8iaNLPPpGtqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这里需要提前配置好你的Outlook邮箱账户(其实邮件是从outlook邮箱发出的)，然后在弹出的窗口中输入收件人、主题和正文，下面是我做的一个示例：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPaNYiciarZZBBZNdXTJOKfA71cS5PDKd8Gia7ALzb6CEEDxaGibKzV84tLB2zmMAcc2KalfEBu8Z48kw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

在这里可以输入任意邮箱，并且可以同时给多人发送邮件，正文部分还可以插入动态的值，比如指标数据、日期以及仪表板的链接等。

至此设置完成，当刷新报表达到警报的阈值时，不仅会在PowerBI服务的通知中心看到提醒，指定的收件人还会收到来自Outlook的电子邮件：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPaNYiciarZZBBZNdXTJOKfA7dAAxxmiaYyBNlQgLoRK655lZXb0YqSmOBW4OZTSWqkXGquZsXO8DfPA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

利用这种方式，即使手机上没有安装PowerBI App，甚至没有PowerBI账户的用户，也能随时随地接收重点关注的指标信息了。  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
