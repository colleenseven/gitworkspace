---
create_date: 2021-12-02T12:51:41 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI业务分析：折扣计算问题
source: https://mp.weixin.qq.com/s/97BWgmBnqjbia90TZfF5ug
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

本文介绍一个经常会遇到的折扣计算问题，我曾被很多人问过类似的计算，这里我通过一个简化的数据，介绍在PowerBI中实现折扣计算的思路。

假设订单表结构如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqxdeEBL5q7tj0xHxiaoVJ8gofrapf3EgVJ2f9H9gpFqMcs30GdyM3y6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

记录有每个产品在各个平台上的原价和每日销售数量。

另外还有一个折扣表，记录了促销期间每种产品在各个平台的折扣率：

**每个平台上的折扣不同，并且促销起止日期也有差异，如何通过以上两个表快速计算各种维度下扣除折扣后的净销售额呢？**

下面是实现步骤。  

**1\. 构造模型**

构造模型是PowerBI数据分析的基础，先梳理需要分析的维度，建立合适的模型，而不建议拿到数据，直接就利用这些表开始写度量值计算。

就以上的分析需求来说，分析维度是三个：日期、平台和产品，所以先做三个维度表，都可以利用DAX来生成。

日期表制作很简单，以前专门介绍过：[玩PowerBI必备的日期表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)

平台表和产品表都可以从订单表中抽取不重复的数据作为维度表，比如产品表直接这样写就可以了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqNLyJKSIF9WPUM0KxVLXmvqfbhzfGTKBlmtDNDIJXtuTLqcAbgE2y8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

维度表做好以后，可以这样来建立模型：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqacH6SngeXTT3uVcNwY5rr54sib5WDIsGUS3ok34DI8yOaMHkibFF31XQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中日期表与折扣表并不存在直接的对应关系，就不用建立关系了，利用DAX来实现日期的查找，下面会看到。

**2、建立度量值**

首先写一个基础度量值来计算折扣前的原始销售额：  

> 毛销售额 \= 
> 
> SUMX('订单表','订单表'\[单价\]\*'订单表'\[销售数量\])

然后是折扣率的计算，如何计算出每个订单所对应的折扣率是重点，度量值可以这样写：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqLBmx82AI2ibdZOia1kRLicCjlkCcmu7bj2Ky0eribmzRRCEiaHIU9z50wjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

核心逻辑是通过上下文的信息去筛选折扣表，找出筛选后的折扣表所对应的折扣率。  

有了这个折扣率，就可以计算净销售额了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUqbBsfFEzf2B23WKH697esGKLentsCGMqVmwuX1z6Okf94ibRvtRES5GQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里并不能简单的用毛销售额乘以折扣率来计算，因为如果没有明细的上下文，是无法准确的计算折扣率的。这个度量值中SUMMARIZE返回的表，是构造折扣率计算所需要的内部行上下文，无论外部筛选上下文是什么，在这个度量值内部，总能提供包含日期、平台、产品维度的上下文。  

并且这样的写法也能确保总计等于明细行之和。

**3、展示计算结果**

完成了上面的步骤，最后这一步就非常简单了，选择合适的可视化类型展现就可以了。

这里用矩阵来展示结果，将维度表中的字段放到矩阵的行中，毛销售额和净销售额度量值放到值中，就可以利用上下钻取来查看每一个维度折扣前后的销售额。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNtvAKNYHIAkpAcdCBUMIUq1lKLOhy1j2KxDAj7PMrtau1EqYGKzu8ibLfKBQg8cpJ4XdpdL71JmUA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

以上就是PowerBI折扣计算的实现思路，其实各种业务分析，抛开细节的业务逻辑，主要的步骤均是如此，关键是要多思考多练习，做到举一反三。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
