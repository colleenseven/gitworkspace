---
create_date: 2021-01-29T20:19:35 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI如何计算不同期间的共同客户?
source: https://mp.weixin.qq.com/s/EDAYA9RLjPCNNBaMPKA3MA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

这是来自星友的一个小问题，他想找出今年的客户有多少，去年同期的客户有多少，以及两个期间的相同客户有多少？  

关于计算每个期间的客户数，比较简单，但是计算共同客户数量他就不知道怎么计算了？难道要把两个期间的客户导出来，然后再匹配哪些是相同的客户吗？

当然不需要这么麻烦，使用DAX可以很轻松的计算出来，以PowerBI星球的示例数据模型为例：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3LfVYKZNOrk4FTzZdhJnybxacP48diaXpF4PWaVfOW5VA5vicXVkcjKibJV6tNvro5x6WENdEqxICA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下面就来计算本期与去年同期的相同客户数量，计算本期的客户，可以这样写：

> 客户数量 = COUNTROWS(VALUES('订单表'\[客户姓名\]))

这里用订单表中的客户姓名，而不是客户表的原因，是它可以根据上下文对订单表的筛选，自动计算该上下文环境下的客户数量，如果用客户表，则返回的永远是总体的客户数量。

有了本期客户数量，上年同期的客户数量用时间智能函数可以这样写：  

> 客户数量 PY = 
> 
> CALCULATE( \[客户数量\] , SAMEPERIODLASTYEAR('日期表'\[日期\]) )

本期和去年同期的客户数量用表格显示如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3LfVYKZNOrk4FTzZdhJnyutn1s40S5ln3kUTRdMfR9Mlwx6V7yZzdyFjCzTo4wiaulRCjyR0KRGw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就看看如何计算共同客户数量，其实就是本年的客户与上年客户的交集，当然不用把两个期间的客户列表先展现出来，依然只需要一个度量值：

> 共同客户数量 =
> 
> VAR customers=VALUES('订单表'\[客户姓名\])
> 
> VAR customers\_py=CALCULATETABLE(VALUES('订单表'\[客户姓名\]),SAMEPERIODLASTYEAR('日期表'\[日期\]))
> 
> VAR customers\_same=INTERSECT(customers,customers\_py)
> 
> RETURN COUNTROWS(customers\_same)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3LfVYKZNOrk4FTzZdhJny6TJCG8iaOyibschQRZpWEr13dbo12mcMDYBLcxpXHXon05bV3nEkpMfQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

根据上图的注释，应该很容易明白这个度量值的逻辑，先利用VAR定义本年客户和上年客户的表，当然这两个表都是虚拟表，然后用INTERSECT函数计算出两个表的交集，最后用COUNTROWS函数计算交集表的行数，就是共同客户的数量。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3LfVYKZNOrk4FTzZdhJnyv4aHt8j0EGTmxbTf2I31fkicTJCv6Cb9vUoUP2zzopicXCib1EicxeRic7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里关键是虚拟表的使用以及INTERSECT函数，VAR定义的变量不仅可以是值，还可以定义表，并且利用VAR定义变量之后，可以避免多重函数的嵌套，步骤更加清晰，对于理解度量值的逻辑很有帮助。

而INSTERSECT函数用于求两个表的交集，并且可以接受虚拟表作为参数，利用它可以很方便的计算出相同的客户列表，有的人不了解这个函数，所以卡到这里了。  

上面是以同期对比为例来计算共同客户的数量，对于任意两个期间的计算，逻辑都是相同的。

这个例子很简单，但类似的困惑可能很多人都遇到过，使用PowerBI时遇到某个特定的计算，自己逻辑也清楚，模型也会建，但就是做不出来，也许只是因为你不知道有个DAX函数就是专门做这个运算的，所以了解更多的DAX函数，可以帮你更高效的解决问题。

共同客户数量计算出来了，如果还想列出每个期间的共同客户都是哪些，怎么做呢？下篇文章接着说。  

___

**PowerBI星球的**[**历史精华文章合辑**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)**：**  

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNn5eia186067w5or6WoVmwdm210CYQfaibhdzFvJvR59sFUgk13iauEzR4oLzGvXiaziaX8VJcB2sCbzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

___

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和 3k+ 学习者一起成长
