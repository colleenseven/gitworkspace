---
create_date: 2020-11-19T23:46:46 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI交互技巧：利用按钮实现跨页钻取
source: https://mp.weixin.qq.com/s/yuEUXvD0ugClkUVYPA5m3w
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

钻取是PowerBI中常用的交互方式，不仅可以对某个图表进行上下钻取，还能够跨页钻取来查看详细信息，之前的文章介绍过跨页钻取的做法：

[深入了解Power BI的跨页钻取功能](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069310&idx=1&sn=7097550bfc21942b1120b613a5acd2f1&chksm=8e0c4969b97bc07fc38f6f19716b9df7b6505d9ae57785a8152297b28dcf8c3bb832cc0da928&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNfCnYMnPkx1uIN2d7bL9KcibbWqKmGruBOKjcuUsxUW4wSZibq6B0ibGJ7quiaUK8U4ZmeggmOjjn0Gw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这种做法是利用右键单击视觉对象，来实现钻取的，如果用户对PowerBI不熟悉，可能发现不了这个交互技巧，有没有更合适的方法呢？

本文介绍另外一种跨页钻取方式，利用按钮，来钻取到目标页面。

其中前三个步骤和[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069310&idx=1&sn=7097550bfc21942b1120b613a5acd2f1&chksm=8e0c4969b97bc07fc38f6f19716b9df7b6505d9ae57785a8152297b28dcf8c3bb832cc0da928&scene=21#wechat_redirect)一致，都是要先建好待钻取的目标页，不同之处仅在于最后的交互方式，所以前面的步骤不再重复介绍，如果你还不熟悉，请先看看那篇文章。

依然用前面文章的示例，假设待钻取的目标页已经建好，这里建了两个页面，名称分别为：树状图明细页和柱状图明细页，下面来看看操作步骤。

**1、在页面上插入一个空白按钮。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMicjW8cK4icCeVFF37tpoXOCRTUSlu2uWbVMg4Q7Q5yibLBcvdmuLH7NtRxzVicc3Vnty1x7vozNqRTQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以按喜好修改按钮的文本、颜色等，按钮文本可以设置为：_查看明细数据_。  

**2、设置按钮的操作属性**

将操作类型设置为“钻取”，并选择一个目标钻取页：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMicjW8cK4icCeVFF37tpoXOCcmYHuCxiaribib29hQyWZAdvgCyibQsR6FRTFpq8llK23gtQMCQglENwIg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3、点击按钮钻取**

按钮设置完成后，当没有选择数据点时，这个按钮是灰色的，将鼠标移上去，将提示你如何使用：

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

然后单击图表中的某个数据点，按钮就会激活，按住Ctrl键点击即可钻取到目标页。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMicjW8cK4icCeVFF37tpoXOCsSJRBTTpaZ9wchVhHuibxOY2zF4OpgGfnl5GBLEBEbiaerbR4gUYCiaeQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

上面就是利用按钮进行钻取的简单示例。

**当有多个目标页，利用右键钻取时，可以选择某个页面，但利用按钮，如何选择页面呢？**  

同样可以利用页面的可视化控件来实现动态钻取到目标页。  

首先，建立一个目标页名称的结构表，如下图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMicjW8cK4icCeVFF37tpoXOCiauayJLUPRfyDaRdoiaib8VlPXED4q7Grt9Ejicx1E42ZsricIuEfib2ESaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并利用这个字段，在页面上生成切片器。  

然后，建立一个度量值，来动态获取切片器的选项：  

> 钻取目标页 \= 
> 
> IF( SELECTEDVALUE( '类型表'\[类型\] ) = "树状图页面",
> 
>     "树状图明细页" , "柱形图明细页" )

打开钻取按钮的操作属性，点击目标页面旁边的条件格式fx，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMicjW8cK4icCeVFF37tpoXOCEjiaK3dla46WVyLJVsDX3pqK9PIZCk4cpnlKwFwwKzMibJ00ljbnqdMA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在弹出的窗口中选择刚建好的度量值：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMicjW8cK4icCeVFF37tpoXOCI8w2ibN3eofWRTO2YvV4MMctBdkVKXVT3Qic8qpnWItnLgjE32JXdQRA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

至此交互设置完成，页面上除了按钮，还有个切片器：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMicjW8cK4icCeVFF37tpoXOCCpulOk5BjnHzyhcV8KJJWzshIrM5FKTVOK1SToKgyyBK9fWgC9VBNA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

想钻取到哪个目标页，就先选择切片器，然后点击“查看明细数据”按钮即可实现。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMicjW8cK4icCeVFF37tpoXOCSH1V8932oTULNsAxK4fdjkjjgmq9lESpIB7ohydBGp5CfMT99gzt3Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

如果您希望钻取动作更加明显，让用户更方便的操作，则可以尝试创建钻取按钮，来提升报表交互的可发现性。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，与2k+ 学习者一起成长
