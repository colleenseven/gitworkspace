---
create_date: 2021-01-31T20:19:11 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI如何动态展示表？送你两种方法
source: https://mp.weixin.qq.com/s/RgQvlImxcXEl_9RaqnNs3Q
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

日常分析中，我们不仅需要动态的计算一个值，常常还有动态返回表的需求。生成一个表，直接的想到就是利用DAX新建表，但计算表的属性是静态的，它无法与可视化页面上的筛选器交互，所以无法满足动态化的需求。

而度量值是可以动态交互的，但它只能返回单个值。

度量值和计算表都不能动态的返回表，那是不是在PowerBI中无法实现这个需求呢，当然不是。

首先要解决动态的需求，这就只能靠度量值了，关于返回表的需求，可以利用度量值来间接实现。

以[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074587&idx=1&sn=99d29ab05054ec2d5e439b6296ad53a3&chksm=8e0c528cb97bdb9a68012f98ddc5042b33c273e46816b01d89079704416cce2638ef5e413f0e&scene=21#wechat_redirect)（[PowerBI如何计算不同期间的共同客户?](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074587&idx=1&sn=99d29ab05054ec2d5e439b6296ad53a3&chksm=8e0c528cb97bdb9a68012f98ddc5042b33c273e46816b01d89079704416cce2638ef5e413f0e&scene=21#wechat_redirect)）提到的共同客户为例，如何动态的返回每个月的共同客户列表呢？

介绍两种利用度量值间接实现的方式。

**1、利用度量值将表的数据连接成字符串，将表变成一个值**

由于度量值只能返回一个值，而共同客户是一个列表，有很多客户名称，要想变成一个值，可以通过CONCATENATEX函数，把列表的数据连接起来，变成一个合并字符串，这样就可以利用度量值来返回了。

度量值如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPoT4k4an0MEQe427woeQye7f8QH7LxOpcWLzhzNCpzud1kajHmBOdibdaAxUklMtLoMF2hXGpObbw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个度量值的前7行与[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074587&idx=1&sn=99d29ab05054ec2d5e439b6296ad53a3&chksm=8e0c528cb97bdb9a68012f98ddc5042b33c273e46816b01d89079704416cce2638ef5e413f0e&scene=21#wechat_redirect)中共同客户数量的写法完全一致，只是最后一行RETRUN的结果，前面是用COUNTROWS来计算共同客户列表的行数，而本度量值是把共同客户列表中的每个客户利用分隔符"/"连接起来。

然后将这个度量值放到卡片图中显示，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPoT4k4an0MEQe427woeQyeIhic7szGtc8VonlZ0DSfTVuRdIHoH0JHcEfl958g9uoNbLPnfiaSSqQg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样就变相实现了用度量值动态的返回一个表。

这种方法适用于列表数据较少的情形，如果数据很多，一个卡片图显示不全，并且也不便于阅读和分析，不建议用这种方式，而是下面的方法。

**2、利用度量值作为表的筛选器**

度量值虽然不能返回表，但它的动态结果可以作为表的筛选器。  

对于共同客户，我们还可以这样写度量值，如果该客户是共同客户，就返回1，否则返回BLANK，将这个逻辑用DAX表达如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPoT4k4an0MEQe427woeQyenllTwM3nZ6kBqptvEUBlp5ibosAaTjgWicrcIH8QTlsEAIwtDPO0tDAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**变动的地方依然是最后一行，其实这几个度量值的主体都是先把共同客户列表找出来作为一个虚拟表，然后根据需要对这个虚拟表进行计数、合并或者判断。**

然后利用客户表的客户名称做个表，将上述度量值放到表的筛选器中，只显示值为“是”的数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPoT4k4an0MEQe427woeQyeLfzGHNZCXy9UdchgQLtWmmOVicicspR7iblb3HFfy26kVgs7O8GnAs5SQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPoT4k4an0MEQe427woeQyekYRibH5sRNI2mW9L1Up4zopO3UpicKm2QUx1S0EhRWX6DHiac4NoRnB6A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

不仅只显示客户姓名，你还可以在这个表格中添加更多字段，丰富共同客户的信息。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPoT4k4an0MEQe427woeQyef1icO5Bp1icLGtLdicvK0SqtqmHwbiaD8mKRFm3CXV1QDkOMWz2etmqn4Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这才是我们需要的效果。

所以虽然度量值不能返回表，但是它的动态属性，可以作为表的筛选条件，来间接实现动态表的展现。

推荐使用第二种做法。

___

  

**PowerBI星球的**[**历史精华文章合辑**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)**：**

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNn5eia186067w5or6WoVmwdm210CYQfaibhdzFvJvR59sFUgk13iauEzR4oLzGvXiaziaX8VJcB2sCbzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

___

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
