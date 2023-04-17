---
create_date: 2020-09-09T20:39:26 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI数据建模，为什么不建议你使用双向关系？
source: https://mp.weixin.qq.com/s/uYYC3YB9fnKMU8IqqOQx9w
author: 陆文捷
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

> 文/陆文捷
> 
> 物流供应链优化分析师，Power BI爱好者，知乎:Beethovenist

经常有伙伴会在星球中询问在数据模型中，如何通过事实表对维度表筛选计算的问题，此类需求在PowerBI中启用表之间双向筛选配合度量值可以解决。

但在复杂的数据模型中开启双向筛选会对度量计算产生让使用者难以察觉的影响。本文就此结合案例，和大家一起揭开这一隐秘的角落。

假设模型如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvC21ib0JbUMibZQw7cz0DbXZMDKupqYhO4IHwnLzSmrrEWU7y3fhm67e0g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

数据模型由不同维度表和销售订单/采购订单建立的一对多关系。分别对客户\[客户名称\]和 产品\[产品子类别\] 字段建立切片器，此时这两个切片器无法互相筛选。

因为当前模型中这两张表都是作为一端对多端的事实表进行筛选，尝试将‘产品’和‘销售订单’两表间的双向筛选激活：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvCMmc37fJj9rSX00OOmh8NXK7H8XyNGc6KAViaIK9hsdpahrZG5CYsHaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

此时物理模型间的箭头也同时指向了两端

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvCDrXlUK1Ul90KKbzV1ic1AK4pzhgXtJqzVcpT2TdmuB3OZN4YeKibVwuA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

开启前两个切片器均显示全局数据；开启后选择不同客户时相应的产品子类别也在动态变化，不难理解双向筛让‘客户’表的数据通过‘销售订单’表能够对‘产品’表的数据进行筛选。是不是很方便？

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvCrfQMF6LRNK4eawlbRErkWhBj9icZ3GhPoA858Ocb9hfxicRgI4LVNnxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvC3lw52vSD63SSw0S6iaEuhqZSIpRFNzTyThGI0eFYXlm5D3hiafnzIOIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

再次观察数据模型，发现此时的‘日期’表’筛选采购订单表有两条路径：

-   直接路径：**‘日期’->’采购订单’**
    
-   间接路径**：******‘日期’->’销售订单’->’产品’->’采购订单’****
    

**Power BI对这类多条路径指向同一目标表的情况通常会自动选择具有最短传递层级的那一条**，也就是‘日期’->’采购订单’的直接路径。很自然，也很智能的做法。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvCatoGGiaXwzGPFCDff0JduNZJEV8DLpYhUhIMkYiaESkpqYSxiaM94Yh6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

那么双向筛选是不是解决各类表与表之间的相互筛选的良方？激活所有的双向筛选就可以一劳永逸了？

不妨基于更为复杂的模型创建度量值验证上述疑问。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvCFFUOEicjpHktGD2yBySicb63eXbMnHic2cicUVApniaV0m7kbUv8gQugfJQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

根据数据模型，用三种颜色标记三条数据筛选的流向，

**1、‘客户’表会对‘采购订单’进行筛选**

**2、‘日期’表会对‘销售订单’进行筛选**

**3、**‘日期’表会对‘采购订单’进行筛选****

特别注意：**‘日期’和‘客户’表会同时对‘销售订单’进行筛选，也同时对‘采购订单’进行筛选，**那么此时如果用日期表来筛选采购订单表：

**Power BI还会通过最短路径（****3深****蓝色线路****）执行筛选吗？**

**还是会通过销售订单的的间接路径关系进行筛选？**

**又或者两者兼用？**

实践是检验真理的唯一标准，创建度量值来验证下吧，

> 采购数量 = SUMX( '采购订单' , \[数量\] )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvCpzHl1of0yQpglwysNMGFGwPTkv23TDAuDib2RAMD0q51vKK239ria2Zw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

‘客户’\[客户行业\]->‘采购订单’表的筛选路径为标注的蓝色线路；‘日期’\[年份名称\]-> ‘采购订单’表的筛选路径同时有两条起作用：**标注的深蓝色线路**以及借由‘日期’表与‘销售订单’表之间的关系（**标注的橙色线路**）进而间接地对采购订单表的筛选。 

利用CROSSFILTER函数断开日期表与采购订单表的筛选看看是什么结果：  

> 采购数量.无日期-采购订单筛选 = 
> 
> CALCULATE( 
> 
>     \[采购数量\] , 
> 
>     CROSSFILTER( '日期'\[日期\] , '采购订单'\[发货日期\] , None ) 
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvCotVRzibaRTpT6TtJArz2oaaTYaiaBJMgfO1DlcAywaBjBvGicAKHuStaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

用CROSSFILTER取消日期表和采购订单表间的筛选，‘日期’\[年份名称\]和‘客户’\[客户行业\]对采购订单表的筛选全都经由销售订单表这座桥梁来完成。计算结果发生了变化。

同样的方式，如果断开日期表与销售订单表的关系，又会变成什么样的结果呢？

> 采购数量.无日期-销售订单筛选 = 
> 
> CALCULATE( 
> 
>     \[采购数量\] , 
> 
>     CROSSFILTER( '日期'\[日期\] , '销售订单'\[发货日期\] , None ) 
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMc1GOicgicLibHUhj6EWR2VvCf7Zvg8xQy67zf5YG3k6hSJZtFzvgCwXT1ODLx8NiammwflLo93vxCXg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这一次是取消日期表和销售订单的筛选，你变我也变~，当然又是不一样的计算结果啦。

注：CROSSFILTER函数作用是更改表之间的筛选流向（SINGLE-单向，BOTH-双向，NONE-取消筛选）。

**实践结论：**

由于销售订单表和产品表双向筛选的存在，使得模型中同时有两条路径能让日期表对采购订单表进行筛选。

**当使用CROSSFILTER取消 日期-采购订单 或 日期-销售订单 的任一筛选传递，日期表会根据另一条有效路径对采购订单进行筛选；**

**不作任何处理时，两条路径同时生效。**

不同的筛选传递都带来不一样的计算结果，如果用户没有察觉其中的细微之处，即便定义了符合业务逻辑的计算，也有可能得到背离初衷的结果。

案例中的数据模型有五张表，一条双向筛选，就已经对计算产生多种影响。实际业务场景往往模型更为复杂，某一个筛选流向的变化都可能生出一个数据迷宫。

下一次激活双向筛选前，你是不是要三思而为呢？

**参考文章：**

https://www.sqlbi.com/articles/bidirectional-relationships-and-ambiguity-in-dax/

示例源数据来自于@BI佐罗老师PBI练习素材

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.3k+ 学习者一起成长
