---
ZK: Origin
create_date: 2021-11-24T12:53:05 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何用Power BI计算员工在职天数？
source: https://mp.weixin.qq.com/s/fedaI6Lum4RgAJUGC-XeMQ
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

之前曾分享过一个关于在职员工数量的计算案例（[如何用Power BI计算在职员工数量？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070488&idx=1&sn=71e79fd2fca11e048061b7f1ea2718d1&chksm=8e0c428fb97bcb998f116bcae6c1ca7f4ae493ebbee9778eed0161a16985124e30c11ca08dba&scene=21#wechat_redirect)），最近又有星友问到另外一种相关的计算，如何根据每个员工的入职日期和离职日期，计算每个月员工的在职天数？  

这种计算在人力资源管理中也很常见，这里以下面这个简单的数据为例，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPqialuwryxPZ47aTHW5MHaX85BH2TQ8mSdDQ6W6RKWClexxIsoPSpibeREGjoEdaviaxn188B4ic1duQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

根据这个员工表的信息，统计一个员工的当月在职天数并不难，关键是要判断各种情况下，动态的计算出每个月的在职天数。

下面来介绍一种计算思路，实现步骤如下：

**1\. 建立数据模型**

因为要按时间点计算，所以建立一个单独的[日期表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)是必要的，并且日期表不需要与员工表建立关系。

**2\. 创建度量值**

需求是统计每个员工的某个月的在职天数，那么员工姓名、月份应该作为筛选器来动态选择，利用度量值获取当前的上下文，结合员工表的信息来进行计算。

关于计算的思路和逻辑都已体现在下面这个度量值中，并在代码中做了详细注释。

这个度量值并没有用到复杂的函数，也没有复杂的逻辑，关键是考虑清楚各种情况下，应该用哪些日期进行运算。

如果你先把这个计算逻辑想明白了，其实DAX就是上下文信息的加减运算而已。

**3\. 展示计算结果**

选择一个月份，利用表格就可以展示出每个员工的当月在职天数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPqialuwryxPZ47aTHW5MHaXrQQPQDwscjlEhYictDfSnz0EPZ4uEYq7TejO7PibRicJhHdibFjepkoNSQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

或者将员工与日期表中的年月作为矩阵的行列标题，一次计算出每个员工各个月份的在职天数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPqialuwryxPZ47aTHW5MHaXXic4p5XpPa6Kod3QCNv05VbxepMLPDbIqdEm9pVaRyoYuQBxLibkoLLw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就实现了快速、动态计算每个员工每个月的在职天数的需求。

上面度量值用到的DAX并没有难点，关键是要理解上下文，知道什么是上下文，以及如何获取上下文的信息，并根据这些信息进行各种情况下的逻辑运算。

更重要的是要明白自己的业务逻辑，就这个问题来说，就是要知道如何根据入职日期和离职日期来确定在职天数。很多人遇到问题不会用写DAX，觉得DAX难，深究起来，其实是缺乏思考、懒于思考，自己都没有真正想清楚计算逻辑，和DAX有什么关系呢？

DAX只是个工具，它可以帮你将具体的业务逻辑快速、动态的转换为计算结果，但是它无法代替你思考~

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
