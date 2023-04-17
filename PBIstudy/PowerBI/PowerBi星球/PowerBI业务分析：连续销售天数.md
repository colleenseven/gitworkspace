---
create_date: 2023-04-10T23:25:24 (UTC +08:00)
tags: wx/pbi/DAX函数 
aliases: null
pagetitle: PowerBI业务分析：连续销售天数
source: https://mp.weixin.qq.com/s/W4fGVLlKqntH8zFOrK8Jww
author: 采悟
status: 已完成 
category: 精读文章 
notes: False
ZK: Origin
uid: 
---

DAX:: MAX, ALL, MAXX ,FILTER ,EXCEPT,CALCULATE ,VALUES 

为了衡量业务的连续性和稳定性，会用到连续销售天数这个指标，这种需求也经常被人问起，这里就这个话题来看看如何用DAX快速实现这种需求。  

以下面这个简易的订单表为例：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM0CfZjagLFLEknhd6MJxC4nKfWRA8dCQCTx3zYU8kQaROPNhrm3Uzej7FnShLNLKExj30bR7CebQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

并[创建一个日期表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)，建立如下的模型：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM0CfZjagLFLEknhd6MJxC41V6rhuOyE0smtHZicaeSVn5h3AqEZBXicgTkkSt07ibCPm1PkrH8CA0GA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后写一个度量值：

```
续销售天数 = 
VAR A=MAX( '日期表'[日期] )    //当前上下文的日期
VAR B =ALL( '日期表'[日期] )  //不受上下文影响的日期表中所有日期的列表
VAR C=ALL ( '订单表'[日期] ) //不受上下文影响的所有订单表中的日期列表
VAR D=EXCEPT(B,C)          //获取没有销售的日期列表
VAR E=              //从没有销售的日期列表中，找出当前日期之前的最大日期
    MAXX(
        FILTER(D,'日期表'[日期]<=A),
        [日期]
    ) 
RETURN INT(A-E)
```

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM0CfZjagLFLEknhd6MJxC41CMXdibclSFoFQ7RpeAzibTvIHRVbXmzoicIuZcgb84KtJPgOq5P8mP9w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于这个度量值，用的函数很简单，基本思路是==每个销售日期与上一个未实现销售的日期相减，就得到了这个天==数。

以上公式通过VAR定义变量分步实现，已经在注释中详细列出每个步骤的逻辑和实现目的，你可以结合上下文仔细理解。

然后用日期表中的日期作为上下文，你可以看看这个度量值的结果：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM0CfZjagLFLEknhd6MJxC4eeggwialrSRkkpR9feThOyrWZNPsSzhdZrkhP3uvFtylUrQNk8Ciaebw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

利用这个度量值，就可以计算出每个日期是连续销售日期的第几天了。

如果想计算出最大连续销售天数是几天，只需要再写个度量值，利用MAXX找出连续销售天数的最大值就可以了。  

> 最大连续天数 =
> 
> MAXX(
> 
>     VALUES('日期表'\[日期\]),
> 
>     \[连续销售天数\]
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM0CfZjagLFLEknhd6MJxC4ogibeibV4jbdUzu2IicoNYtC1Urtx4BBpia8t1005N7xRc1Swj9TjVcibMA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常简单呢？  

其实关键是想明白业务逻辑，然后用DAX表达出来。这种计算也不仅仅是计算连续销售天数，使用的场景很多，比如HR管理中的连续打卡天数、质量管理中的连续无故障记录等等，都可以参考这个分析。

最后留个思考题，如果要计算连续增长的天数，应该怎么做呢？你可以先想一下，下篇文章介绍~
