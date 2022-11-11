---
aliases: null
create_date: 2022-02-27T12:21:47 (UTC +08:00)
tags: 
pagetitle: 学会使用PowerBI的“数据警报”，随时跟踪业务指标
source: https://mp.weixin.qq.com/s/b-9vy5mirxS7eNCnYCQJBA
author: 采悟
status: 未阅读
category: 
uid: 
---

本文来学习一下如何在PowerBI中设置数据警报，以便在业务数据指标超出设置的标准时发出通知。

数据警报可以在 Power BI 移动应用和 Power BI 服务中的仪表板中设置，Power BI Desktop 不适用，而且只支持仪表、KPI 和卡片图这几个视觉对象。

以下面这个报表为例：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPtueAYDpXRn54Ss9oMJmVxKq5MeskstYYegHn93UQKxiaNqKplPHibEJMPUxq3hvlK1I4OY4oHlezQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

假如需要跟踪销售情况，如果销售额超过25万时，让系统自动发送通知提醒，下面来看看具体如何操作。  

首先将它发布到PowerBI服务中，打开这个报表后，当鼠标悬停到某个视觉对象后，就会看到有个“固定视觉对象”的按钮：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPtueAYDpXRn54Ss9oMJmVxH8rvjibQV58cxzKGHXwl06UdMhtlQBj4dOIdo7MA2VbwxSIUYo1sLow/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

固定视觉对象，就是将报表的视觉对象，固定到仪表板上，点击这个按钮，会弹出这个窗口：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPtueAYDpXRn54Ss9oMJmVxNaYjELLBlzWKhicv25b8DBicy2H736n361OdPmSESFHZwt6egaYtpb5Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这里我们新建一个“产品经营分析”仪表板。  

你还可以根据需要固定其他的视觉对象到这个仪表板中，然后转到仪表板中，就可以看到固定在这里的视觉对象：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPtueAYDpXRn54Ss9oMJmVxnF98EQ6ia7McCibq4bXC2gFBz5RgS6IvkELxXEZKwbO2dHyUdnOgWnmQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

在这个仪表板中，可以对销售额指标的卡片图添加警报，点击该卡片图右上角的三个点，选择“管理警报”：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPtueAYDpXRn54Ss9oMJmVx2ExklZxS0ol8mEWdabS5RMtriaQINmDkzJHK8CztkiaHYboNNLeOnfOA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

在警报面板中，添加一个新的警报，设置警报标题、条件、阈值以及通知频率：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPtueAYDpXRn54Ss9oMJmVxicmjoQIvjUHLCG0lfgz6M2xqFTPkiacHBT14cI7O6t7uGiaELN4vFSdqQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面的设置，就是当销售合计超过25万，发送通知（其中"条件"选项中文翻译的很别扭,那两个选项你可以理解为高于/低于）。  

然后当报表刷新，销售合计超过25万时，就会在通知中心看到一条通知：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPtueAYDpXRn54Ss9oMJmVxNJiadPgeL8UPicBE7jIV2S7t5pX2Z2ljGLQ81pfMtrOuvAZ7Uia2hKvew/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

并且在上面的警报设置中，还勾选了“同时向我发送电子邮件”，所以在邮箱中同时也会收到一封提醒邮件，显示如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPtueAYDpXRn54Ss9oMJmVxtoAqicm9FShqpBWChicPf48voS6RfRaylQASmbPqDkUS5QbeCSc3xdvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

邮件中不仅有关于该警报的信息，还可以点击链接，直接进入该仪表板查看更详细数据。  

不过上面的方式只能给自己发送邮件，如果想给任意其他人发送邮件通知，可以配合Power Automate来实现，下篇文章接着介绍。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
