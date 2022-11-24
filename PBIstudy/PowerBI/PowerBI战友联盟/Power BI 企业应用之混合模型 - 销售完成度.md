---
create_date: 2022-01-10T13:37:22 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 企业应用之混合模型 - 销售完成度
source: https://mp.weixin.qq.com/s/8uxmKgWq5TL8uoAs2psbjA
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

本文介绍企业混合数据模型。后续将开始介绍相关细节。

## 什么是混合模型

先来看一个图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOrIeYI7x6QY8I7xKVGasOTNg7MkXO2Da0Xz441TqVnAp3TQMjSYicTjhF0BMTQbs6fd4Lc5rA2MFQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个图的特点是最右边的图表与左边的表的连线是 “开口” 的。

这种开口的关系表示了一种 “混合”。

如果某个数据模型已经预先建立并发布到云端运行，用户在使用该模型时，额外关联了模型外的数据，就形成混合模型。

## 应用场景

混合模型，特别适合应用在企业内部已经在云端建立了 Power BI 数据集后，在各个业务部门有自己新的需求而和原有数据模型融合使用的场景。这个场景也被商业智能领域的专家誉为：商业智能的终极形态必备特性。

我们举一个实际场景来说明这个特性的关键之处。

【场景】管理销售目标的达成。

企业已经发布了统一的销售数据模型，并每日更新，业务部门用户可以通过该数据模型每天知道实际的销售进展。该数据模型已经位于 Power BI 云端的 Premium 工作区。业务用户可以通过 Power BI Desktop 连接，并使用该数据模型中的内容。

## 操作方法

前提条件：

混合模型，一般是企业级应用，特别适用于已经使用了 Power BI Premium 的大型企业，这些企业已经由 IT 团队搭建了统一的大型 Power BI 数据集，业务用户可以通过 Excel 或 Power BI Desktop 使用。

但在这个场景下，业务用户希望可以加入自己的内容。

打开 Power BI Desktop，【主页】【获取数据】选择【Power BI 数据集】，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOrIeYI7x6QY8I7xKVGasOTY6SMBoKiab7EnkC73y9ibfgq0mQZ1KFoBBvg2rhIsibiay4n2fYIQZ4mOg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

选择一个云端的数据集，进行连接，完成后即可使用。可以在右下角看到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOrIeYI7x6QY8I7xKVGasOTPtXZddUPayOcxKP4szqIjs8Sau3S56TXhGfdco3H8W7kGmpLGbXvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

整个数据模型如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOrIeYI7x6QY8I7xKVGasOTBmwa6uicIHr60VVbodD1VtFfpSp11vmc3aVssbLdcBTg4QCHICibczog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看出数据模型都是蓝色的。其图标如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOrIeYI7x6QY8I7xKVGasOTnmWPHibQjzo9RJqcnkNScAoOJ6l7ibDGn7ZyrIWEdEYeLUxvqxlzUZdA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

该图标表示此表位于云端的模型，数据源类型是：SQL Server Analysis Services 数据库。

## 加入本地数据

仅仅使用云端数据模型，可以：

-   新建度量值
    

但却不可以新增计算列等，这也是合理的，体现了终端用户不能破坏企业统一数据模型结构的设计思想。而终端业务用户是需要增加自己的数据以完成自己的目的的，例如：加入一个销售目标表，来核算当年的销售进度，这将需要：

-   利用云端原有数据模型的销售数据
    
-   利用本地业务目标数据
    
-   新增计算目标达成的度量值
    

点击【获取数据】后，系统会提醒：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOrIeYI7x6QY8I7xKVGasOT3pP6nwiapWiaibqick3flR497F7iclpfiaoneM1nOVj6Y2TMU6Nka4Grw14g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就会使用 DirectQuery 连接到远程的云端数据模型。

选择一个销售目标表，加载后，通过连线建立关系，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOrIeYI7x6QY8I7xKVGasOT3cDcTOmoA80kllUHdUPpYNvrRH1BKCxO0hYOU1LVejMS7ZwKtPX15Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，这两个表之间建立了关系。这个关系非常神奇，它跨越了云端和本地不同位置的数据。

## 完成计算

实现指标计算是容易的，这里就不再展开，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOrIeYI7x6QY8I7xKVGasOTLfz5Tbf8mOwYDwibypK6D8I5ozCBmQumqfuYSGJcQbr1cIMgHERQG5g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 总结

混合模型，为 Power BI 的大型企业应用提供了重要的基础，本文介绍了销售如何混合远程数据和本地的销售目标来跟进销售的完成。还有更多重要而实际的应用，例如：企业已经有了产片 SKU 的统一分类标准，但在不同市场又有自己的标准，如何混合这些数据实现产品分析，我们后续再做介绍。

**Power BI 终极系列课程《BI真经》**

与精英一起讨论 Power BI，验证码：data2022  

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
