---
create_date: 2021-02-17T20:17:45 (UTC +08:00)
tags:
aliases:
pagetitle: 如何用 PowerBI 做盈亏平衡分析？原来这么简单！
source: https://mp.weixin.qq.com/s/disPuVqLT_hcDhFObXvLqA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

盈亏平衡分析是研究固定成本、变动成本、销售数量、销售价格与利润之间数量关系的一种方法，也被称为量本利分析，是企业进行价格制定、销售计划、盈利预测等经营活动的重要工具，经常有星友问我如何用 PowerBI 来实现，这篇文章就来介绍一个简单的盈亏平衡分析模型。

假设某个产品预测计划中，有单位变动成本、前期固定投入和销售毛利率三个变量，在不考虑其他税费的情况下，达到什么销量才能实现盈利呢？  

PowerBI实现的效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNysmaegt4ibdQN5ql5predfiaibTJRVlYCsZlZhlKoZ45Od53z8dic48VNZ48L3MjpjabBc0rRwgIc3Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

根据这几个因素的调整，盈利状况动态变动，通过这个模型可以快速找到盈亏的临界点，也就是盈亏平衡点。

并且还可以直观看出盈亏平衡点与这些因素的关系，随着某个因素的调整，平衡点呈现正向或者反向的变动，比如固定成本投入越高，盈亏平衡点越高，亏损的可能性越高；而毛利率越高，盈亏平衡点越低，也就是盈利的可能性越大。  

其实做起来很简单，下面简要介绍一下制作步骤。

**1、生成变量参数**

利用PowerBI中的参数（参考：[创建PowerBI「参数」轻松搞定动态分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067672&idx=1&sn=1a141b81b4e20f83cabf410164f55974&chksm=8e0c778fb97bfe9904d988eb9972b26436c260e575d008d1414076b86df997fee74dc559ec73&scene=21#wechat_redirect)），生成单位变动成本、固定成本以及毛利率三个变量，并自动在页面上增加三个切片器。  

销售量同样可以利用参数来生成一个列表，并利用这个表作为坐标轴，但并不需要销量的切片器，生成以后删掉就行。

**2、建立度量值**

盈亏平衡分析，主要是呈现收入、成本、利润随着销量的变动趋势，所涉及到的主要度量值如下。  

因为生成参数的时候，已经自动生成了几个基础度量值\[单位变动成本\]、\[固定成本\]、\[毛利率\]和\[销量\]，其他度量值可以直接套用。  

> 变动成本 = \[单位变动成本\] \* \[销量\]
> 
> 总成本 = \[固定成本\] + \[变动成本\]
> 
> 收入 = DIVIDE( \[变动成本\] , 1-\[毛利率\] )
> 
> 利润 = \[收入\] - \[总成本\]

关键是盈亏平衡点的确定，直观的逻辑是收入曲线和成本曲线的交叉点，也就是利润为0对应的点，**但在实际情况中，可能并不存在利润正好等于0的点，所以这里将盈亏平衡点的逻辑定义为利润非负的最小值所对应的点。**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMzJ7iaOplcBL1b0aMdtB9YV1TYp3DneHJY7TaMcnTvS5LChWFsKd0UIPWkp2nxPts6OoDLIdu8icfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

找出盈亏平衡点以后，计算该点对应的销量和收入就很简单了：  

> 盈亏平衡销售量 \= IF( \[收入\] = \[盈亏平衡点\]  , \[销量\] )
> 
> 盈亏平衡收入 \= SUMX( ALL( '销量' ) , \[盈亏平衡点\] )

至此，主要的度量值建立完毕。

**3、制作可视化**

有了上面的度量值，找到合适的图表展现出来就可以了，本来盈亏分析模型用简单的折线图就可以实现，但为了显示出一条垂直线来直观看出盈亏平衡点对应的销量，折线图无法加这条线，所以这里用了**折线和簇状柱形图**来解决。

将\[盈亏平衡销售量\]放入到该图的【列值】中，其他度量值放入到【行值】中，即可生成一个简单的盈亏平衡分析。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMzJ7iaOplcBL1b0aMdtB9YVCib7P06s4QjWEztpAn8KegJF4rB3SW5iawMZkYaLgtcPdtg000QPWRIw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

完成这个图表需要熟悉掌握PowerBI组合图的各项格式设置，比如按系列设置数据形状，但在细节的处理上，PowerBI还不够丰富和灵活，这个模型中的某些数据标签，就难以通过格式调整来实现，你看出是怎么做到的吗？

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
