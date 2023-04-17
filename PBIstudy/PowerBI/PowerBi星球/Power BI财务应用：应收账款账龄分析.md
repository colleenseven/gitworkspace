---
create_date: 2021-06-18T19:52:23 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI财务应用：应收账款账龄分析
source: https://mp.weixin.qq.com/s/iNzfzzlz2xKWC4ORztNwSw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

应收账款管理是财务管理的一项重要内容，为了随时了解客户的欠款情况，对应收账款进行账龄分析表是一种基本分析方法，这篇文章就先介绍一下如何利用PowerBI，自动生成应收账款账龄表。

假设有一张常见的应收账款明细表，记录了每个客户的每月应收发生额和回款金额等数据，如下图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8sKNEiaM5gw4A48pChyCCBsT1iaE42CRr5agWZMicNrDIzIfLibUHf1wqxJh8uVwHibkqwXhALPYHyXA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

根据这个明细表，如何计算出每个客户的账龄分布情况，比如30天内的应收账款有多少、半年以上的账款有多少、一年以上的应收账款有多少……？  

下面就来看看PowerBI如何实现这种分析。  

**1、建立数据模型**

虽然数据表只有一个表，但是为了分析的需要，我们应建立对应的维度表，在这个例子中，因为需要按客户和时间分析，所以至少应该建立客户表和日期表。

并且为了能够把应收余额分解到不同的账龄中，还必选建立一张账龄分组的辅助表，这里假定按这6种账龄类型，制作账龄表如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8sKNEiaM5gw4A48pChyCCBQhK01FUhMEupick9iaGq8o6jlEqP9Wic7172ICuYHGKLmKgiaoDVbUt87A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后将客户表、日期表与应收明细表建立关系，账龄分组表无需与应收明细表建立关系，模型图如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8sKNEiaM5gw4A48pChyCCBsIGyVxtzqHXatXmx8IRiaMj7um6ibxBD9VatjQE1tj0TAUbLic4IntPjg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于日期表和辅助表的制作请参考：

[Power BI 日期表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)  

[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)  

**2、利用DAX生成账龄分布表**

**基本思路是，先将每个客户的应收余额，分配到实际发生的期间，然后根据发生期间来放置到对应的账龄中。**  

首先建立两个基础度量值，来计算客户的应收发生额和应收余额：

> 应收 本期发生额 \= SUM('应收明细表'\[本期发生额\])
> 
> 应收 本期余额 = SUM('应收明细表'\[期末余额\])

截至到现在的应收余额就是最后一个记账日期对应的余额，但每个客户的最后记账日期并不一致，所以需要先计算出最后的记账日期：  

> 最后记账日期 =
> 
> CALCULATE(
> 
>     MAX('应收明细表'\[记账日期\]),
> 
>     ALLEXCEPT('应收明细表','客户表'\[客户名称\])
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8sKNEiaM5gw4A48pChyCCBwRf90iaNfibFjpjGbHhoSOgibwPzKSbRPlU1VnQsfcibdibxPR5iccfdJiazw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

根据最后记账日期，就可以计算出应收余额：  

> 应收 期末余额 \=
> 
> CALCULATE(
> 
>     \[应收 本期余额\],
> 
>     FILTER(
> 
>         ALL('日期表'),
> 
>         '日期表'\[日期\]=\[最后记账日期\])
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8sKNEiaM5gw4A48pChyCCB58lJKGruOVoSv2Pe7XEYO7mepatz2WVyKoolvZyTPFLzu6Rc4TJ1Uw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后根据应收余额和应收发生额，来计算每期应收未收的金额是多少，度量值如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNWN8YIa3j60NGDTllhuicUvNXVMFPiauRzZctcZRQJg5Gia8pKF4o9IL5aPia8zrhAdwFNJwIXvIY1KQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中的计算逻辑，已用注释说明，熟悉应收的同学应该很容易理解，如果是按月查看客户的应收未收金额，就可以将年度月份放进来：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNWN8YIa3j60NGDTllhuicUvAgWibuePUIAWGto8bEpUibRv5lZ8SUVWgocmia17yic6j52GUHKxROpt5g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有了每期的未收金额，就可能很轻松计算出账龄分布情况了，其实就是分组分析（可参考：[Power BI 数据分析应用：客户购买频次分布](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070056&idx=1&sn=f03cc79148b1c420d25800be8c0380b9&chksm=8e0c4c7fb97bc56943e3552d9403aaf07e1bb12b24f8f248aab2891af38614f1065e289697e7&scene=21#wechat_redirect)）：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNWN8YIa3j60NGDTllhuicUvHQqdlwicLlwKOibGiaDwYPjv2ibRqLqxlCodibYeVuGGdzNxYydib3iaRdic0A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

做个矩阵，将客户放到【行】，账龄放到【列】，上面的度量值作为【值】，就能自动计算出每个客户的应收账龄分布情况了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8sKNEiaM5gw4A48pChyCCBOIgDtS1ItCnQUL25zOKr2QiaQudCq1DJM5LEnwvdW3uBNIwMwicibzia2g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里有问题是，总计金额不正确，可以单独修正一下，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8sKNEiaM5gw4A48pChyCCBBIdlM7Jlib2mb9OQkDuRdYSJkibnvl3ON7mERJYtUWUlAKDRt1CdBEgw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参考：[Power BI 总计错误的终极解决方案(二)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072950&idx=1&sn=fdd3128f59f1797c5a1dad976604f0bb&chksm=8e0c5b21b97bd237c39d1afb7e89f7b453c4fc12b09456aaaca57dd83dbf3e71208752d11b6a&scene=21#wechat_redirect)

把这个修正后的度量值放到矩阵中，就是正确的结果了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP8sKNEiaM5gw4A48pChyCCBLz5tBrvcJpeQKficYGvAicu7b5OhQetvwicXFPMQibUrOLX7VX2AdFDmqw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就自动生成账龄分布情况，如果应收明细表数据有更新，只需要点击刷新，即可自动完成每个客户的应收账龄分布，一目了然的掌握每个客户的欠款情况，关于账龄分组，可以根据实际需要来调整。

其实账龄分析也是一种分组分析，掌握了分组的逻辑，实现起来并不难，上面的这些度量值的逻辑需要你仔细理解，首先应该先想清楚业务的计算逻辑，然后学会用DAX来表达。

很多人不会用PowerBI做复杂点的数据分析，其实多数情况下并不是PowerBI或者DAX太难，恰恰是因为没有真正想清楚业务的计算逻辑。能不能先分解问题，并用语言描述出来计算逻辑非常关键。

___

**618限时优惠活动进行中**

扫码立减50元，PowerBI星球社群最后一次这么低价，感兴趣的星友不要错过了哦~  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNKwl8qibtr4ZxJ7WPtps7CJMHA1vEqTmWWpyDWxfbMJPiamUDJiaJHCKugTdIyLfpUmhWLofHFS3tBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

老会员如果已经到期或者即将到期，也可以扫码使用会员专属5折续费卡：

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

**如果你对PowerBI星球社群还有什么疑问，可以添加采悟微信（powerbi001）咨询。**

**▼****点击****阅读原文****，也可立享优惠~**
