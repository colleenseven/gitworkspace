---
create_date: 2021-06-14T19:52:44 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI数据分析：如何快速找出连续下降的数据？
source: https://mp.weixin.qq.com/s/SbouH0J_ge829-O65NLl-Q
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

源于知识星球中遇到的一个问题，星友想通过PowerBI，找出最近3个月销量持续下滑的产品都有哪些？这个问题比较典型，也很实用，所以这里写篇文章介绍一种思路，希望对你有所帮助。

最近3个月数据持续下滑，**可以转换为最近3个月环比持续为负数，**那么在计算逻辑上，**就可以先计算出环比，然后统计某产品最近3个月每个月的环比，小于0的数量，如果等于3，那么就是最近3个月连续下降。**

以常用的这个产品销售数据模型为例，找出最近3个月销售持续下滑的产品有哪些？

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOM5Yibb67GTg4DCibsnNEqAMuHFdKjrQ9EgnL4dlh2Q6u6pnJeStysGmTKcj0LWv8DSmwxWv5Eib6Ig/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

先写几个基础度量值来计算环比：  

```
本月销售 = SUM( '订单表'[销售额] )
```

```
上月销售 =
```

```
环比 = DIVIDE( [本月销售]-[上月销售],[上月销售] )
```

然后写一个度量值来判断每个产品是否持续下降：

```
最近3个月是否持续下降 = 
```

主要的逻辑已经在度量值中做了注释，其基本思路就是本文开头提到的逻辑，用DAX代码表达出来就行了。

这里用N作为一个变量，可以灵活控制最近N个月，如果需要动态的N月控制，同样可以使用参数来控制，无论是多少个月，都可以通过这种方式快速计算出连续下滑的产品，比如将N改为2，就是最近2个月连续下降的产品。  

利用产品名称做个表格，将是否持续下降的度量值放到筛选器中，只筛选结果为1的数据，即可动态显示满足条件的产品（参考：[Power BI如何动态展示表？送你两种方法](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074639&idx=1&sn=03b003d199f754794c0bac8af15c50e0&chksm=8e0c5258b97bdb4e0aa92667a047bca5c7705f86a6c2b4ac66e3eefc171ca95e6891a433ecff&scene=21#wechat_redirect)）：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOM5Yibb67GTg4DCibsnNEqAMz7ficNhf5GVKaPia5E7D607gFxZQiavVjqibvicekfEulxDwVHSxict31edw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

掌握了这个思路以后，其实不只可以计算持续下滑，持续上升同样可以按这个思路，比如也可以统计消费持续下滑/升高的客户，绩效持续恶化/增长的员工等，都可以帮我们快速找出经营异常的数据。

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

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
