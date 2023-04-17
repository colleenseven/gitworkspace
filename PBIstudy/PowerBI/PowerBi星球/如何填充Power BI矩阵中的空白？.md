---
create_date: 2021-07-15T19:42:13 (UTC +08:00)
tags:
aliases:
pagetitle: 如何填充Power BI矩阵中的空白？
source: https://mp.weixin.qq.com/s/pLWNH57LnADPFziJ3pEVvA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

经常会遇到这样的问题，如何对可视化的表格或者矩阵中出现的空白，进行向下填充数据？从PowerBI功能上来说，并没有这个设置，无法直接对可见的单元格数据进行操作。

但从数据的计算逻辑上并非不能实现，就是让空值等于上面最后一个非空数据，可以用DAX来完成这种填充。

以下面这个简单的数据为例：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOnO9AvQ7yMSh2jcANicJ7YvNYMoTyaQZJtu1VDTSDeiaSicLfA1ssM3kQb4bFcHgE8moFb39Q8ibqfOw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为并不是每天都有数据，所以如果用个连续的日期表作为矩阵的行，类型作为列，就变成了下面样式的表：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOnO9AvQ7yMSh2jcANicJ7YvypWYP3DIbDVGOIB1v4ibeVth9qR1nZmxrQOvhclu3FoXliaZt5sXfP4Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样的矩阵是不是很常见？对于其中的空白如何填充完整呢？

先以向下填充为例，实际上就是，如果某天的数据是空值，就让它等于该日期之前的最后一个非空数据，建一个度量值，用DAX表达如下：

```
今日数量 = 
```

主要是利用了DAX函数LASTNONBLANKVALUE的逻辑，这个函数通过对已排序的列对应的表达式求值，返回不为空的表达式的最后一个值。

上面的度量值的逻辑，就是对日期表中，先筛选小于等于当前日期的日期，对每一个满足条件的日期计算数量，返回最后一个有数据的日期所对应的数量，结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOnO9AvQ7yMSh2jcANicJ7YvzRuibVAf2npfT1nJnicXsuOpWayWHfclq3OIicNwqL5JG9J86ibJX4VCjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是向下填充的效果。  

同理，如果想向上填充，也就是让空值等于之后日期的第一个非空的数据，可以用FIRSTNONBLANKVALUE来实现，它与LASTNONBLANKVALUE的用法完全一致，只是逻辑正好是相反的，返回第一个非空数据。  

```
今日数量 = 
```

向上填充的效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOnO9AvQ7yMSh2jcANicJ7Yvk7TtMUic853pMyIehZicTPHJqTptsBk4SAiaAdqkXEoJjQSPdqeSfrzmw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果你也有类似的填充需求，可以试试用上面的思路来实现。

不过LASTNONBLANKVALUE和FIRSTNONBLANKVALUE也是一种迭代函数，如果你的数据量较大，应该谨慎使用这些函数，以免影响报告的性能。

___

**[新书上市：PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
