---
ZK: Origin
notes: True
aliases: null
create_date: 2022-09-22T23:26:49 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: PowerBI如何进行工作日的滚动计算？
source: https://mp.weixin.qq.com/s/pBFu48ruYhrjfzRTOOSXew
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

DAX:: SUMX, FILTER, ALL, MAX, AVERAGEX

---

之前的文章中介绍了滚动指标的计算（[_Power BI 滚动聚合_](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069714&idx=1&sn=82ec558b5ef6bf991dc0de0e3a3ead79&chksm=8e0c4f85b97bc693f113d2e9bc425c405b2ab2f1a3f93d8546073265c22f099a4994f1d2acd8&scene=21#wechat_redirect)），最近被问到，如何只对工作日进行滚动计算，比如<mark style="background: #FF5582A6;">最近7个工作日的滚动求和</mark>，这种用PowerBI怎么做呢？

关于工作日的分析，之前也分享过相应的文章：  

[如何用Power BI进行工作日相关的计算？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077728&idx=1&sn=5d7739914cb98e96b7abd32d402aba3e&chksm=8e13ae77b96427615638ed7351de474f87095c983d3d5c745b94ed1c0fc35a87e34ea247683d&scene=21#wechat_redirect)  

其实将上面两篇文章结合起来，就可以实现工作日的滚动计算。

首先依然是需要完善日期表，在日期表中添加工作日相关的字段，具体添加方法见上面关于[工作日分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077728&idx=1&sn=5d7739914cb98e96b7abd32d402aba3e&chksm=8e13ae77b96427615638ed7351de474f87095c983d3d5c745b94ed1c0fc35a87e34ea247683d&scene=21#wechat_redirect)的文章。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtAKbaX23icHwagk7mmSoVQcA7rJzfZgVjyeNKcic1lSFKQHBHAOOvus7Wg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

工作日的滚动计算，对于这种<mark style="background: #FF5582A6;">不规则的日期区间无法直接使用时间智能函数</mark>，不过使用最基本的函数也可以完成，<mark style="background: #FF5582A6;">滚动求和就可以用SUMX+FILTER组合</mark>。  

> 7个工作日滚动求和\=
> 
> SUMX(
> 
>     FILTER(
> 
>         ALL('日期表'),
> 
>         '日期表'\[工作日编号\]<=MAX('日期表'\[工作日编号\])&&
> 
>         '日期表'\[工作日编号\]>MAX('日期表'\[工作日编号\])-7&&
> 
>         '日期表'\[工作日标记\]=1
> 
>     ),
> 
>     \[收入\]
> 
> )

这个度量值的逻辑就是利用<mark style="background: #FF5582A6;">FILTER函数来找出最近的7个工作日期</mark>，然后<mark style="background: #FF5582A6;">SUMX函数将这7个工作日的数据累加起来</mark>。  

这样实现了工作日的滚动7天求和：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMucXInVVsJkvBiaichaT4gV5GTQhWRTupc8R0GC8QfXptiacrwh2ic4hLkbiaL5MecAmCefan0ySqfT2g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上是工作日的滚动求和，如果是想计算工作日的滚动平均，只需要将SUMX函数变为AVERAGEX就可以了。

比如<mark style="background: #FF5582A6;">30个工作日的移动平均</mark>是这样写的：

> 30工作日移动平均 \=
> 
> AVERAGEX(
> 
>     FILTER(
> 
>         ALL('日期表'),
> 
>         '日期表'\[工作日编号\]<=MAX('日期表'\[工作日编号\])&&
> 
>         '日期表'\[工作日编号\]>MAX('日期表'\[工作日编号\])-30&&
> 
>         '日期表'\[工作日标记\]=1
> 
>     ),
> 
>     \[收入\]
> 
> )

用折线图展现如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMucXInVVsJkvBiaichaT4gV5MImkIicGxPwRq3juwHLU4ibAwcO4iaaCJbTGelTRa1IxCnmibiazcjUIx3w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于移动平均，也可以参考：[你做的预测不靠谱？是因为你不知道用移动平均！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068131&idx=1&sn=650477c6ae71dd9b6d1d31f55b37db21&chksm=8e0c75f4b97bfce2b76ac4c5e102501bae16d37701355f0f96a3f4df1a59337e1b8b858a28b6&scene=21#wechat_redirect)  

同理，对于计算最近N个工作日的最大值和最小值，也是改一下聚合函数，SUMX改成MAXX/MINX就可以实现。

关于工作日的滚动计算，关键点是在日期表中构建关于工作日的相关列，然后就是与自然日期类似的计算思路。
