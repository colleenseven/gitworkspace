---
ZK: Origin
notes: Fa'l'se
aliases: null
create_date: 2022-01-04T12:33:02 (UTC +08:00)
tags: 
pagetitle: Power BI数据分析入门案例：目标实际对比
source: https://mp.weixin.qq.com/s/xASouv-y6venMHVB1Oszfw
author: 采悟
status: 未阅读
category: 
uid: 
---

平时大家的学习，大都是在一个预先设计好的数据模型基础上，进行各种分析，有些星友说看书或者看文章感觉理解了，对应着操作一步步也可以做出来，但是拿起自己的数据想做个分析，发现还是不知从何做起，真是所谓的"一看就会一做就废"。

这其实是没有真正形成PowerBI的分析思维，所以我挑选了几个常见的场景，再详细介绍一下PowerBI分析思路和具体步骤，这篇先来看看目标实际对比案例。

假设有两张表，一个是每日销售表，一个是每月目标表，模拟数据如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOm979TXruJWZHVXibA13nZN71oOZMtDe4txCKP5zPFhNFmicEpse6Jic8VWwVCHd9NURibtyMq15I8VA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

类似这样的问题我经常碰到，有星友直接发给我这两张表，问怎么写度量值，来**计算每个月每个产品的目标完成情况？**

这是很常见的数据结构，对于熟练使用PowerBI的人来说，这个非常简单，一个简单的数据模型就实现了，但是对于初学者来说，很可能就不知道从何下手。

在介绍这个分析之前，先就这个问题看看初学者两个常见的误区：  

**误区一：PowerBI数据分析就是写度量值**  

就像上面的问题，上来就问这种分析如何用DAX写度量值，其实更重要的是建立数据模型，在模型的基础上，才能进一步的考虑要不要写度量值，如何写度量值。

**误区二：数据建模就是对现有表建立关系**

有些人也知道要建立数据模型，但是如何建模就完全没有思路了，只盯着现有的表，就像上面的销售表和目标表，这两个表到底该怎么建立关系呢？看起来好像通过产品名称来建立关系，但是这样建立关系以后，下一步还是不知道怎么做。

其实数据建模并不仅仅是针对已有的表，而是要根据分析的需要，梳理现有表的结构和相互之前的关系，提炼出分析的维度，如果缺少独立的维度表，就建立维度表，然后再建立关系。  

下面来详细看看这个问题的解决步骤。  

**1、根据分析目的完善数据结构**

这一步是建立数据模型的准备工作，上述业务的分析目的是按月查看每个产品的目标完成情况，可以看出有两个分析维度，产品维度和日期维度，就需要建立两个维度表：产品表和日期表。  

将原始数据导入到PowerBI中以后，可以直接在现有表的基础上利用DAX构造维度表，产品表可以这样来建，在数据视图中点击新建表：

> 产品表 = VALUES('销售表'\[产品名称\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOm979TXruJWZHVXibA13nZNkh2uWEMvz3So72VrA1EveYJKuNRKSrJjf2RPdOCvRftPJEpFBf9DDg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就建好了一个产品维度表，实际上就是所有产品的不重复列表。  

日期表之前介绍过多种制作方式（[玩PowerBI必备的日期表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)），你可以任意选择一种方式来建，记得要建完整年度的日期表，而不是仅根据业务起止日期来建。

关于日期还有个问题，销售表的时间维度是日期，而目标表的时间维度是月份，并不在同一个粒度上，为了与日期表建立关系，建议为目标表添加一列日期，比如该月的第一天，同样可以用DAX新建计算列来完成：

这个刚建好的日期列是文本型，记得要改成日期型：

字段数据类型非常重要，建模之前要仔细检查关键字段的数据类型是否正确。

**2、建立数据模型**

通过上面的准备工作，现在有4张表，原有的销售表、目标表，以及新建的产品表、日期表。为了便于区分，一般将产生数据的表称为事实表，比如销售表和目标表；而作为分析维度的表称为维度表，就是上面新建的产品表和日期表。  

数据建模一个基本的原则是事实表之间不要建立关系，而**通过维度表与各个事实表建立一对多的单方向关系**，这4张表可以这样建立关系：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOm979TXruJWZHVXibA13nZNnicujC20EGwD2b3l0LsOo9YSvRibINXiasza7fsyFG6aR6SrFJjn9zIXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是一个简单的星型模型。建议你在建模时，尽量参考上面的原则，星型模型是PowerBI中的最佳模型结构。

**3、展现分析结果**

有了上面的模型，计算每个月每个产品的实际销量和目标销量，只需要用个矩阵，将日期表的年度月份、产品表的产品名称放到矩阵的【行】中，将销售表的实际销量和目标表的目标销量放到矩阵的【值】中：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOm979TXruJWZHVXibA13nZN1szrmZu8MicBfUxDezIMoHj2OcchuuibQvMeyBbdnIOuicj0OPYicjooJQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

完全没有写度量值就可以完成计算。

如果进一步计算目标完成率，可以写个度量值：

> 目标完成率 \= 
> 
> DIVIDE(
> 
>     SUM('销售表'\[实际销量\]),
> 
>     SUM('目标表'\[目标销量\])
> 
> )

放到上面的矩阵中结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOm979TXruJWZHVXibA13nZNcakpH6b0PNLEjY1GibEBzgTWsJJTDBvCm6gicG3vuWTs8FaE7UxfoPVQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常简单！  

这就是PowerBI数据模型的强大和便捷之处，建好合适的模型，只需要鼠标拖拽字段、以及很简单的DAX就可以实现分析目的。

如果你觉得一个问题，虽然业务思路很清晰，但是在PowerBI里不知道该怎么分析，或者分析起来非常别扭，大概率是你的数据模型没有建好。  

希望这个简单的案例能帮刚开始学习的伙伴，打破固有的不合理思维，真正认识到数据模型才是PowerBI数据分析的灵魂。

[**PowerBI星球的最新版****内容合辑****，值得你收藏学习：**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)  

[![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN8YOicNXzCaSLpQrKXOL0LsNeYw0fj3iaGFy7XSwwmibHicdtiaHEbhgmHSPXQlkg3WiaVA4hJ8PGDcdEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
