---
create_date: 2023-04-10T23:24:52 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI业务分析：连续销售天数
source: https://mp.weixin.qq.com/s/W4fGVLlKqntH8zFOrK8Jww
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

为了衡量业务的连续性和稳定性，会用到连续销售天数这个指标，这种需求也经常被人问起，这里就这个话题来看看如何用DAX快速实现这种需求。  

以下面这个简易的订单表为例：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM0CfZjagLFLEknhd6MJxC4nKfWRA8dCQCTx3zYU8kQaROPNhrm3Uzej7FnShLNLKExj30bR7CebQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

并[创建一个日期表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)，建立如下的模型：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM0CfZjagLFLEknhd6MJxC41V6rhuOyE0smtHZicaeSVn5h3AqEZBXicgTkkSt07ibCPm1PkrH8CA0GA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后写一个度量值：

```
连续销售天数 = 
```

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

关于这个度量值，用的函数很简单，基本思路是每个销售日期与上一个未实现销售的日期相减，就得到了这个天数。

以上公式通过VAR定义变量分步实现，已经在注释中详细列出每个步骤的逻辑和实现目的，你可以结合上下文仔细理解。

然后用日期表中的日期作为上下文，你可以看看这个度量值的结果：  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

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

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

是不是非常简单呢？  

其实关键是想明白业务逻辑，然后用DAX表达出来。这种计算也不仅仅是计算连续销售天数，使用的场景很多，比如HR管理中的连续打卡天数、质量管理中的连续无故障记录等等，都可以参考这个分析。

最后留个思考题，如果要计算连续增长的天数，应该怎么做呢？你可以先想一下，下篇文章介绍~

___

[PowerBI星球的最新版内容合辑，值得你收藏学习：](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

[**「PowerBI星球」内容合集(2022版)  
**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083365&idx=1&sn=7acb9794552bbd59387c0c39ee2767f5&chksm=8e13b072b9643964fb7ee25b1ccb32d30143567bb780626f963166ea599d90f6dc8ee77154a2&scene=21#wechat_redirect)

___

  
**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
