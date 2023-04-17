---
create_date: 2020-09-16T20:37:59 (UTC +08:00)
tags:
aliases:
pagetitle: 处理多对多关系，Excel中的PowerPivot与PowerBI哪个更方便？
source: https://mp.weixin.qq.com/s/mupkunG64VrhAJINxxO8Vw
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

在现实业务场景中，难免会遇到多对多的数据关系(Many to Many)，例如：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRpGahA2U6WYuvUGV2Kiax13atqKzssDFFjeP7yXbYkibCeI71E65AR5VQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个产品维度表部分产品同属于多种产品类别，它与事实表之间的关系就是多对多的关系，下面来看看在PowerPivot和PowerBI中，分别是如何处理多对多关系的？

**PowerPivot**

在Excel的PowerPivot数据模型中直接用\[产品名称\]或\[产品类别\]列与事实表建立关系会报错：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRtsKHicMDh9Xc6lWfqksnJpVnPwap7pIpib99P1JhiacodpVfQsJwsAadg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为目前Power Pivot还不支持直接建立多对多关系，解决这一问题的常用方法是通过中间表（bridge table）解除多对多关系的耦合。

先分别建立产品和类别表，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRnRsibnXPjDG1wP4Xnd6KN5Nf3Y11oAerV2QgIrj7qcibh5o55wu4vIxg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPIM5zuFE4vRuzm6rL8m9I4RuwgZ6npibgwReYicMshtCTLqwMEg1XCPZP60rtkqEkDKyia11WXRkNSw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

产品-类别对应关系组成中间表，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRq2aNADGXkBGdEj4FvqShFTS1dfSKhmicUPnjWBgptaqWyucdVpO3Ttg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)  

建立这三张表对应的**‘产品(新)’→‘产品类别’，‘类别’→‘产品类别’**一对多模型关系，原来含多对多关系的产品表就此解耦，拆分为三张表，如下图所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWR08sSJJmQ8n9AJniczSAxU9Z7ibwUIKevvX4FiaSL8jXaIaqRbeQvShvuw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

新构建的完整模型关系：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRzHIF7RQZCSIeh55yviaLBJ2AFziaeG3EFP7r9FEYoQc89p2sAQUjCKsA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

建立度量值

> Gross Margin \= SUM ( '订单'\[毛利\] ) 

并按 ‘产品 新’\[产品名称\]汇总：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRTvqBzCthTuzqtp9zhrW76nvYhtj0ShiabCvja423BrmslofXtoO3blw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不惊喜不意外，一切还是那么自然。

然后按照\[产品类别\]汇总数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRUDkrNJMcYrL5sIDQShUPyppnktRUGRwbTABXk6pznTowYhE1Lz6dOQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

咦？！每个类别的汇总数字都是总计数，显然不对了。再观察下数据模型，\[产品类别\]无法通过传递对事实表形成有效筛选，故在明细类别和总计行上都返回全局汇总结果。

故事当然不会再此终结，隆重有请CALCULATE和中间表来帮忙：

> Gross Margin New \= 
> 
> CALCULATE( \[Gross Margin\] , '产品类别' )

结果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRenoP5ISicM5bv8FbfUGgicNvej7lSja5JB3yiaibHo0kJ9QcI3BuVavGDg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将中间表作为CALCULATE的表筛选参数，开启了数据从**‘产品类别’→‘产品 新’**表间的多端向一端的流向。

Excel 2016以后的版本新增了CROSSFILTER函数，更为容易理解的度量值写法可以实现同样效果：

> Gross Margin CROSSFILTER\=
> 
> CALCULATE( 
> 
>     \[Gross Margin\] , 
> 
>     CROSSFILTER( '产品类别'\[产品名称\] , '产品 新'\[产品名称\] ,BOTH ) 
> 
> )

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRciab75JL6oibRVLGUw9gczeD7dIqc0zVOP071SkI4JrbyX69IZCIpDEA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从关系图来理解，解锁橙色箭头的数据筛选流向是正确汇总的关键。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRZNOJPDyrRYTVljYdLgEDjPicLPd8ia9bUwfEHvL8gLRsT8jzplTXvPVg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

那么在PowerBI中如何处理多对多关系呢？ 

**Power BI**

在PowerBI Desktop里，处理起来简单许多，无需建立中间表，也不用借助CROSSFILTER，Power BI天然支持多对多关系并且还提供不同的筛选选项：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRsicdlhib4Kv9vkgXE1MdU22mhqfEZrM1uLaAGEZaicaBIVBticSx1mU1bA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

 设定多对多关系，选择数据筛选方向配合度量值轻松搞定：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRcoLBYiceZWpdkOQkeIoRpYphdwjRePu0vtnJ0vtrib2fYBO7yWeXgz3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

相比Excel是不是方便不少？

当你建立多对多关系时，**Power BI还会提示用户若非完全知晓计算意图和潜在影响，多对多关系并非数据建模的标准做法。**

另外数据筛选流向有三种选择：

-   正向：产品→订单
    
-   反向：订单→产品
    
-   双向：产品⇄订单
    

本文案例用正向和双向筛选都能返回正确结果，参考之前关于[双向关系](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073049&idx=1&sn=3443f6b0c1d60cb5f3100b0fc96e34bf&chksm=8e0c588eb97bd198ad64607e4390aae225f679f08abc35a05a8a5202d1d9b81e68e9f3c5a235&scene=21#wechat_redirect)的文章，在此还是建议启用单一筛选流向。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNMfCshhicHKypAgS54QQVWRBiax0eprXJGIL9tzw0tlXYZ9zL4ArLcCLxvUIDcJQJja3Ppfo10BLAg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**总结**

**PowerPivot处理多对多关系**

灵活使用中间表，掌握CROSSFILTER用法突破Excel无法建立多对多物理模型的限制。

**PowerBI处理多对多关系**

Power BI不仅能照搬Excel的处理方式，建模也为自由灵活，可以直接建立多对多的关系，但建立多对多的关系也要慎重选择哦~

从这里也可以看出，PowerBI的功能要比PowerPivot强大的多，建议大家直接学习和使用Power BI。

**参考文章：**

https://www.sqlbi.com/articles/many-to-many-relationships-in-power-bi-and-excel-2016/

示例数据基于星球案例文件，个人略作调整

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.4k+ 学习者一起成长
