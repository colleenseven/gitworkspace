---
aliases: null
create_date: 2022-04-08T11:55:26 (UTC +08:00)
tags: 
pagetitle: Power BI分析10个常用的业务度量值，你肯定会用的到
source: https://mp.weixin.qq.com/s/54nAF2l3igg5NelDgQ8wIg
author: 采悟
status: 未阅读
category: 
uid: 
---

Power BI业务分析中，经常会遇到类似这样的问题，如何找到最新业务日期、如果找出最大订单对应的客户名称等，本文将大家经常问到的一些基础业务度量值的写法汇总如下，希望对你有所帮助。  

这里以这个简易的订单表为例，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtlq82WF3fDnQ6iaIpic0pvh4ribibsCt84IswIuicTWdCHn49Dv554epWzdg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

先写个基础度量值备用：

销售额合计 = SUM('订单表'\[销售额\])

下面就来看看这些常见业务指标的度量值写法。

**1\. 最新业务日期**

> 最新业务日期 = 
> 
> MAXX(ALL('订单表'),'订单表'\[日期\])

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtM5C58ib6FZsmicbuDKZuiaAZxTBGwib2XXsLjYMibXE6MS6T0u8d3YP6W7w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

利用MAXX从全部订单表数据中提取最大的日期。

**2\. 最早业务日期**

> 最早业务日期 = 
> 
> MINX(ALL('订单表'),'订单表'\[日期\])

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtEkfiaESa7RuNqQMlC1Bibbv4cCiahcrbVdkgvgI1wORxu1QEC6NnjoyCw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

利用MINX从全部订单表数据中提取最小的日期。

**3\. 最新业务日期下单的客户**

> 最新业务日期下单的客户 =
> 
> CALCULATE(
> 
>     MAX('订单表'\[客户\]),
> 
>     FILTER(
> 
>        ALL('订单表'),
> 
>        '订单表'\[日期\]=\[最新业务日期\]
> 
>     )
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWt9pSrZBrq4toxPLRABTg290Q0R5Hw1Nauag18CyA95h7iaszThDaL2gw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

从订单表中筛选订单日期等于最新业务日期的行，然后利用MAX返回该行对应的客户名称。  

**这里假设结果只有一个客户，如果有多个客户，见下面的介绍。**

**4. 最新业务日期上一个交易日**

> 最新业务日期的上一个交易日 \=
> 
> CALCULATE(
> 
>     MIN('订单表'\[日期\]),
> 
>     TOPN(2,ALL('订单表'),'订单表'\[日期\])
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtQaibImPicRQ0OHMYd6Iodibpicc26740s90mHk2oN8vHCS1UbquImp17sA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

利用TOPN筛选最大的两个订单日期，然后利用MIN取其中较小的日期。  

**5. 最新业务日期上一个交易日销售的产品**

> 最新业务日期上一个交易日销售的产品 =
> 
> CALCULATE(
> 
>     MAX('订单表'\[产品\]),
> 
>     FILTER(
> 
>        ALL('订单表'),
> 
>       '订单表'\[日期\]=\[最新业务日期的上一个交易日\]
> 
>     )
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtbVMlCfoICfOa8A5X0tKZ7CfCZ3jO8cjnYDIicY7GPiaqkmUkczzUAtpQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

从订单表中筛选订单日期等于最新业务日期上一日的行，然后返回该行对应的产品名称。

**6. 单笔最小订单对应的产品**

> 单笔最小订单对应的产品 \=
> 
> CALCULATE(
> 
>     MAX('订单表'\[产品\]),
> 
>     TOPN(1,'订单表',\[销售额合计\],ASC)
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtVQ1jlwRrcZjJUvCSQ04jtkia7m7123DqU5Y4XuEeTwd4RJO8Jeicmoxg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

利用TOPN筛选订单金额最小的订单（TOPN最后一个参数ASC,按升序排列，获取最小值的行），然后利用MAX提取对应的产品名称。

**7. 单笔最大订单对应的客户**

> 单笔最大订单对应的客户 \=
> 
> CALCULATE(
> 
>     MAX('订单表'\[客户\]),
> 
>     TOPN(1,'订单表',\[销售额合计\])
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtZ6tgGicsfVibe5BoJDPn5eqPc4f9UauRSODGUicezFUYKoufmGGmQn2gQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

利用TOPN筛选订单金额最大的订单（TOPN最后一个参数省略,默认降序排列，获取最大值的行），然后利用MAX提取对应的产品名称。

**8. 单笔第二大订单对应的客户**

> 单笔第二大订单对应的客户 =
> 
> CALCULATE(
> 
>     MAX('订单表'\[客户\]),
> 
>     TOPN(
> 
>         1,
> 
>        TOPN(2,'订单表',\[销售额合计\]),
> 
>        \[销售额合计\],
> 
>        ASC
> 
>     )
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtSK0ZUABx2NVbIJgr47ibykib2lfp3lQ4aPsxIjFfbJSVicf1H3tXBeN7A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这里的主要逻辑是2个TOPN，内层TOPN返回销售额最大的2笔订单，然后外层的TOPN从其中筛选出较小的那一行。  

**9. 销售额最高的产品**

> 销售额最高的产品 =
> 
> CALCULATE(
> 
>     MAX('订单表'\[产品\]),
> 
>     TOPN(1,VALUES('订单表'\[产品\]),\[销售额合计\])
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtaBxQHV9otUYVdic7HQYMZTg9B2CTGeXS2yrialE3js8VguiaUILQcxh6A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

利用TOPN找出销售额最高的产品行，然后利用MAX返回该行对应的产品名称。

**10. 销售额最低的产品**

> 销售额最低的产品 =
> 
> CALCULATE(
> 
>     MAX('订单表'\[产品\]),
> 
>     TOPN(1,VALUES('订单表'\[产品\]),\[销售额合计\],ASC)
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPD0dHkRQic9LdHtfxEslBWtzSYoKv3FGGFcjbLP91ucvzib4L6z86IibVjpwvVAX6EYSahtc0VmHQAw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

利用TOPN找出销售额最低的产品行，然后利用MAX返回该行对应的产品名称。

但是如果你仔细查看每种产品的销售额，实际上销售额最低的有两种产品。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNgc6NicGicFw8JiajOHKn9jSia5LMU0aU0GU78U8QepWtYibkZdFjaUMaSdZJuOnsszia4tDJg0dCDfAZg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于前面的度量值，都是假设不存在并列的情况，所以直接用了MAX函数，因为对于唯一的值，用MAX或者MIN函数都可以，都是返回这个值本身。

对于并列的情况，如果想随便返回任意一个，那么用MAX/MIN也可以，但是如果需要返回全部的名称，还可以用CONCATENATEX函数将所有的结果连接起来。

以销售额最低的产品为例，将这个度量值修改如下：

> 销售额最低的产品\=
> 
> CALCULATE(
> 
>     **CONCATENATEX(  
>         VALUES('订单表'\[产品\]),**
> 
>         **'订单表'\[产品\],**
> 
>         **"/"**
> 
>      **),**
> 
>     TOPN(1,VALUES('订单表'\[产品\]),\[销售额合计\],ASC)
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNgc6NicGicFw8JiajOHKn9jSiaHA2nyicPNqAwFFX9dlAickbc7vibZnSBfric4vDJmga4ruSACy6kmmPdyw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

当存在并列的情况时，你都可以参考最后这个度量值的写法，将并列的名称利用CONCATENATEX函数组合到一起，同时显示出来。  

这里的示例都很简单，其实大多数的分析，抛开具体的业务背景，都是这些常用的逻辑，或者多个逻辑的组合，用的DAX函数也并不难，常用的就是这几个，灵活运用就可以解决日常遇到的大多数问题。

遇到类似的计算，你也可以直接套用。与日期相关的各种度量值，推荐阅读这篇文章：

[各种时间指标的度量值，让你一次看个够](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069739&idx=1&sn=e8a57761fe68cf5f3a92ed811c314c59&chksm=8e0c4fbcb97bc6aa7391500817c58416077b696acc892b4cb58024d0f23a5031dec2cfd7c14b&scene=21#wechat_redirect)  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
