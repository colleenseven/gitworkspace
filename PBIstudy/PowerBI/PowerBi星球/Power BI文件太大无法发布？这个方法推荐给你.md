---
create_date: 2021-05-06T20:00:29 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI文件太大无法发布？这个方法推荐给你
source: https://mp.weixin.qq.com/s/iOcr3-c7QSQp8QSBNYLyAA
author: 瓶子
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

> 文/瓶子
> 
> 目前从事职考行业的数据运营，喜欢钻研power bi和excel来实现自动化。

最近经常在工作中遇到报表太大发布不了，或者明明使用相同的数据集，却因为要做不同的报告，需另外花费时间制作同一份或基本相同的数据集模型的情况，不知道你是否遇到了呢？今天我就来总结下这个问题，并给出很简单的解决方法。

通常情况下，当我们使用数据导入模式在power bi进行报表发布时，是将数据集模型和报告一起发布的。然而当数据集模型特别大时，有时甚至达到上千兆，而power bi最大支持文件大小为1024兆，过大就会导致发布不了，会出现如下提示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPiaXuRjOnia8xPlzOArdgPicwImPnxWM1djWMsmW1z09icv5U7bTxea68dOgqCg6yhfWiaY2ZMo0XPczQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还有一种情况，当文件不是很大，小于1024兆，而网络比较慢时，也经常会出现远程主机关闭一个现有连接的提示，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPiaXuRjOnia8xPlzOArdgPicwXglTVoNdIrcIegAhHPB5ic100GDt9q4fH6PWN0OjlO8u3foDOria46Ug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

另外，当我们想要在另一个报告使用相同的数据集或数据集的一部分模型时，重新制作数据集模型显然太费时间，即使使用Tabular Editor来批量复制度量值或者表数据也不是一个最优解。

一般情况下，我们制作的报告其实都不大，主要是数据集占的内存大，如果只是发布报告，基本很快都能成功发布，另外在power bi desktop中又是可以直接连接power bi服务中的数据集，然后制作报告。今天就沿着这个思路分享一个技巧，帮你解决上述几种问题。

基本思路就是，先将制作好的pbix文件拆解为数据集和报告文件，然后再发布和使用。

**第一步**：准备一份我们将要拆解的pbix文件，比如下面这个文件。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPiaXuRjOnia8xPlzOArdgPicwke2mzjeiamr7p9iamE80YApTAlrOcVKYbdM3gLYUhRztCkdKdamaudzw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第二步**：另外复制一份该pbix文件，然后将副本中的报告页面全部删除，只留下数据集，然后点击发布，将该数据集发布到PowerBI服务。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPiaXuRjOnia8xPlzOArdgPicw15dfHEBUyIxQEahcHbJRAwSKjDxld4AyKG1c5sZTj5ibPk5bFJZcEFw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第三步**：再复制一份第一步准备的pbix文件，打开副本文件后在建模视图选项卡中将数据集全选删除，只留下报告页面。其中当数据集删除后，报告页面会出现错误提示，可以不用管，继续下一步。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPiaXuRjOnia8xPlzOArdgPicwj5szL1gNibFtuv1XjwquibiaZSDsCVbmIajYcQ4sXg33KeIKZzvzb1tog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第四步**：点击左上方的主页-Power BI数据集，即可看到第二步发布到Power BI服务的数据集，选中该数据集，点击创建，继续下一步。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPiaXuRjOnia8xPlzOArdgPicwiacvS9HxMjstPH5aMBlm8IKFk8KWvcZMB2EItc8eNmyJJ7pnjR22e7Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**第五步**：在进行第四步之后，Power BI会自动刷新数据，等待一段时间，数据更新完成后，会呈现出第一步做好的报告的样子，且右下角显示已实时连接到Power BI数据集。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPiaXuRjOnia8xPlzOArdgPicwBqBqCG82eKDBShIqA4F5ryky8N4HArzA70FgiaQGFcP85POxqs32j1w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

操作完成。

注意点：因为需要将PowerBI数据集发布到PowerBI服务，所以整个过程需要账户登录。

通过将pbix文件拆解成数据集模型和报告，有至少三种优点：

**1\.  在发布Power BI报告文件时，由于删除了数据集，只留下报告页，文件大小变得很小，发布时间大大缩短。**

**2\.  可以在不同的报告中，使用相同的数据集或其中的一部分数据模型。**

**3\.  在发布到Power BI服务后，还可以将数据集共享给其他人，以供其他人使用该数据集。**

回顾整个过程，其实就是使用了Power BI能够连接实时数据集的思路，好像也没那么复杂，是吧!

当你遇到类似问题的困扰时，不妨试试这种方法。

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
