---
create_date: 2021-01-19T20:21:10 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI如何进行财年分析？
source: https://mp.weixin.qq.com/s/vQyctluB5DN567GwJYma-A
author: 采悟
status: 已完成 
category: 精读文章 
notes: false
ZK: Origin
uid:
---

DAX:: TOTALYTD ,IF, QUARTER

日常分析涉及日期维度的分析一般是用自然日历，但也有些比较特殊，比如有些国家/地区的财务报告年度并不是从1月开始，有的是从4月开始，有的是从7月开始，苹果的财年是从10月开始的，这种年度一般称为财年（Fiscal Year），本文就来看看PowerBI如何按财年分析。

按财年分析时，对某个月的计算一般并没有影响，涉及到年度季度的计算时，才需要特殊处理。

比如计算本年累计，并不是常规的从1月开始累计，而是从财年的开始日期累计，假如==某公司的财务年度是从10月1号开始、9月30日结束，本年累计收入的度量值可以这样写==：  

> 收入 FYTD = 
> 
> TOTALYTD( \[收入\] , '日期表'\[日期\], **"9-30"**)

其计算结果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNwdGaD6PCEPcE4mgDCfDAM8ArPaPCPpictR5ibxFkwWSxOhfyar03XhfI6YDKE1Rqf6SN5udichkiaRw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从上图可以直观看出，本年累计数据并不是从1月开始累计，而是从10月开始累计的，正好符合财年累计的计算要求。

通过上面本年累计的度量值，也可以看到时间智能函数对于财年的计算依然可用，关键最后一个可选参数：**年度结束日期**。  

对于==时间智能函数，不仅是TOTALYTD，包括其他几个与年度有关的时间智能函数，都可以通过最后一个可选参数来控制年度的结束日期==，在之前介绍时间智能函数时，也都提到过，参考：[一文了解PowerBI的时间智能函数](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067537&idx=1&sn=b6a0ac62f09fe97ebe530573ad8623d4&chksm=8e0c7606b97bff10157eb8ffde8589acc80ec0118bf9a73ec1acca7a69611525b2453e907dc4&scene=21#wechat_redirect)

虽然利用自然日期表和时间智能函数也可以进行财年分析，但更灵活的方式是==做一个财年日期表==。如果现有模型中已经有了一个日期表，可以直接在现有日期表的==基础上添加相应的财年维度列==。

以财年从10月1日开始为例来添加财年的年度和季度，假如财务年度按这样的逻辑定义，小于10月，则财年等于本自然年度，大于等于10月，则财年等于下个自然年度：  

> 财年 \= 
> 
> IF( \[月\]<10 , "FY"&\[年度\] , "FY"&\[年度\]+1 )

财务年度从10月开始，则10月至12月为第一季度，依次类推：  

> 财季 = 
> 
> IF( QUARTER(\[日期\])=4 , "Q1" , "Q"&QUARTER(\[日期\])+1 )

添加财年字段后的日期表效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNwdGaD6PCEPcE4mgDCfDAMJWtGqCr8NMjQAG3IOInarHe3OCia5LnoIsmpMLHWgkjE22XRqW0N8lw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

利用新添加的财年财季字段，来计算每个维度的收入以及累计收入如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNwdGaD6PCEPcE4mgDCfDAMCbE71yBicA9UGaJicHmzGicQLPYdCQCvyQ2HjQoEsDe61nENMia2uRtSxg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来和正常的自然年度季度并没有什么不同。

如果财年分析中需要按其他粒度来分析，都可以按上面的方式，在日期表中添加对应粒度的财年字段即可。
