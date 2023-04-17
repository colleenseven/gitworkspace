---
create_date: 2021-07-08T19:43:31 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI分析技巧：如何根据起止日期进行数据统计？
source: https://mp.weixin.qq.com/s/fcOsmv5sfxsqeqX2zXRIRw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

最近遇到几个类似的问题，根据项目/合同的起止日期来统计，某时间点或者区间的相关指标，比如下面这个项目数据，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcdDEoeYbmbcMJ9eTlc1f1VM2icjbMuoKPwicuOZibkQo2IhyiblwfnU03pmDJbGF0JkRQl3FwcGkluA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这是我们经常会碰到的数据结构，包含有两列日期，开始日期和结束日期，常见的需求是，**如何按月查看尚未完成的项目有多少，以及对应的项目金额？**

下面就来看看如何利用PowerBI来实现这个需求，步骤如下：

**1，建立数据模型**

因为要按日期来计算，所以建立一个独立的日期维度表是必要的，关于建立日期表的方法见：[玩PowerBI必备的日期表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)  

项目表有两列日期，那么应该用哪个日期与日期表建立关系呢？对于本文的需求来说，其实可以不建立任何关系，模型如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMcdDEoeYbmbcMJ9eTlc1f1U2YrPU1PSqbBaw2xSwk0eohXXmS5hgiag47bjNttjxFguNOn51203tg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2，创建度量值**  

统计每月末尚未完成的项目数量，其逻辑很简单，就是筛选开始日期早于月末，而结束日期晚于月末的项目，度量值可以这么写：

```
期末未完成项目数量 = VAR maxdate_=MAX('日期表'[日期])VAR activeitems=FILTER(    '项目表',    '项目表'[开始日期]<=maxdate_    &&'项目表'[结束日期]>maxdate_)RETURN COUNTROWS( activeitems )
```

**其实这个度量值不仅仅可以统计每月末的未完成项目数量，还能统计任何一个区间，比如每天、每季度末、每年末的数量。**

筛选出符合条件的项目以后，统计未完成项目的金额只需要在此基础上求和汇总就行了：  

```
期末未完成项目金额 = 
```

**3、统计指标可视化**  

可以用组合图展示上面计算的两个指标：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM4TySZ4yJOcQPzq5DtJyYSHWbUia0qIkTGLe2iceSIGK7Dttib8YgFlqYz3P4ed4vRtE6Xj2mphyWiaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是按月查看未完成项目的数量和金额指标。  

如果需要计算每期处理的项目数量和项目金额，应该怎么做呢？这个指标是只要项目经过本期，无论是否到期，都应该统计进去，不仅仅是期末尚未到期的，还包括在本期内到期的项目。

可以在上述度量值的基础上加上本期内到期的项目数据，也可以计算出来，不过显得太繁琐了，这里给出一个更简洁的写法：

```
本期处理项目数量 = 
```

这个逻辑充分利用了本期上下文的第一天和最后一天，以及项目的开始日期、结束日期，将在本期出现过的项目的逻辑，形成这一行表达式：

> MAX('项目表'\[开始日期\],mindate\_)<=MIN('项目表'\[结束日期\],maxdate\_)

如果你不是太明白，可以根据一个项目的实际起止日期和上下文的最大最小日期来推演，更容易理解这个逻辑。

同理，计算本期处理的项目金额度量值如下：  

```
本期处理项目金额 = 
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM4TySZ4yJOcQPzq5DtJyYS4FYWp4jgY21AIHdIuWXNWjP0kCwe9h2RFCCX5JqmI2iblX3Bic2HsqsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上就是解决此类问题的通用模式，理解了这几个度量值的计算逻辑以后，这一类问题都可以迎刃而解。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
