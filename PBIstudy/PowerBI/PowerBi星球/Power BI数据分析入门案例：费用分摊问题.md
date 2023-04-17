---
ZK: Origin
notes: False
aliases: null
create_date: 2022-01-12T12:32:12 (UTC +08:00)
tags: wx/pbi/DAX函数 
pagetitle: Power BI数据分析入门案例：费用分摊问题
source: https://mp.weixin.qq.com/s/-3Arce_ol0d2ZPXsSRByQg
author: 采悟
status: 已完成 
category: 泛读文章 
uid: 
---

上周介绍了一个基础的分析案例（[Power BI数据分析入门案例：目标实际对比](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078691&idx=1&sn=af288fc6a65368973fd64d53fd392a08&chksm=8e13a2b4b9642ba273bd2f6e9b2547048fe0b4c50dfea6188a6a7b7e63aeb3d586d79534a1f5&scene=21#wechat_redirect)），这里我们再以费用分摊的案例来帮你进一步理解PowerBI数据分析的思路。  

假设有两张表，一个是每日销售表，一个是每月发生的费用，模拟数据如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMmjSURwlpb6TZek3OjZ0nmM7Nerib0XT5IEHsiaHV51eiaJtJdwkx2lcRCuQhPBtxlicXSRiaKgj0psug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

需要**将每月的费用按当月销售额的占比，分摊给每个产品、或者分摊到业务员/部门**，应该怎么做呢？其中业务员和部门是层级关系。  

同样按照[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078691&idx=1&sn=af288fc6a65368973fd64d53fd392a08&chksm=8e13a2b4b9642ba273bd2f6e9b2547048fe0b4c50dfea6188a6a7b7e63aeb3d586d79534a1f5&scene=21#wechat_redirect)的思路，按下面三个步骤进行。  

**1、根据分析目的完善维度表**

由于要按照各个维度来分摊，所以先根据现有的表来生成维度表。

**（1）产品维度表**

> 产品表 = VALUES('销售表'\[产品名称\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMmjSURwlpb6TZek3OjZ0nm1ZlP9MYtqHUvRPNAgPoCyseA6W5IpCic9q7Jicrc1DtzXSGpYOz0Suicw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**（2）业务员维度表**  

由于==业务员和部门是层级关系，可以用SUMMARIZE一次性从销售表中提取两个字段==：

> 业务员表 =
> 
> SUMMARIZE(
> 
>     '销售表',
> 
>     '销售表'\[销售部门\],
> 
>     '销售表'\[业务员\]
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMmjSURwlpb6TZek3OjZ0nmAO3PV3BsQPpY0uNXqlLcyda4EwUAupH8Ficsxh3uJiap976QLhAyMIEw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就提取除了全部的业务员以及所属的部门。  

**（3）日期维度表**  

关于日期表不再赘述，你可以参考这两篇文章自行创建：

[玩PowerBI必备的日期表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)

[分享一个更实用的Power BI日期表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076559&idx=1&sn=e00814afa6a2013e3ba3a19cfb575f39&chksm=8e13aad8b96423ce61ca80169b35047204be5c7e4750491f84d7ff327eba9c093c9aa9a829f2&scene=21#wechat_redirect)  

**2、建立数据模型**

通过上面的准备工作，现在有5张表，原有的销售表、费用表，以及新建的产品表、业务员表和日期表。

这5张表可以这样建立关系：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMmjSURwlpb6TZek3OjZ0nmYjriaV9zicPf4FicYcfcla6OBicjAgcDH5ibmxSYibAEZLqKUVJb4T0Yv23Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

三个维度表根据需要，分别与不同的事实表建立一对多的单向关系。

**3、建立度量值并展现分析结果**

有了上面的模型，下面就可以写度量值来计算分摊金额。

为了下面度量值更简洁的书写，先写两个基础度量值：

> 销售额合计 = SUM('销售表'\[销售额\])

> 费用合计 = SUM('费用表'\[费用额\])

为了得到分摊额，首先需要计算出分摊比例，度量值可以这样写：

> 分摊比例 =
> 
> DIVIDE(
> 
>     \[销售额合计\],
> 
>     CALCULATE(\[销售额合计\],ALLEXCEPT('销售表','日期表'\[年度月份\]))
> 
> )

分母只保留年度月份的筛选，是为了计算出每月的销售额合计，其他上下文的销售额除以该月的合计销售额，就是分摊比例。

然后分摊比例乘以当月的费用合计，就是应分摊的费用额：

> 分摊金额 \= \[费用合计\]\*\[分摊比例\]

用矩阵展示如下，将费用分摊到每个产品：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMmjSURwlpb6TZek3OjZ0nm9aK169JpUbibm1mq5ricmwdV3ejyAyTSIKeBDzaTwRRZ1KEFf2MMEb7g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想将费用分摊到业务员和部门，同样是这些度量值，只需要调整上下文，将产品换成业务员就可以了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMmjSURwlpb6TZek3OjZ0nmYFa1W8KX2auDeK0XTrMhUgUzolibxHBBr5StKUuia4TKtmLjeCcnlS6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就实现了任一维度的费用分摊，并没有用到复杂的DAX公式。  

通过这个例子，不仅是学习如何解决分摊问题，还可以进一步的理解度量值的逻辑，它是一个动态的值，通过上下文的切换动态返回当前上下的结果，当然也不要忘了，度量值背后的数据模型，才是数据分析的灵魂。
