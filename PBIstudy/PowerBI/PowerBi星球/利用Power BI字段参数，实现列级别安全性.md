---
ZK: Origin
notes: True
aliases: null
create_date: 2022-06-27T12:30:19 (UTC +08:00)
tags: wx/pbi/数据处理功能
pagetitle: 利用Power BI字段参数，实现列级别安全性
source: https://mp.weixin.qq.com/s/BvzWRrpz_QOygBYgBQteRw
author: 陆文捷
status: 已完成
category: 浏览文章

uid: 
---

DAX:: SUM, NAMEOF

---

> 文/陆文捷
> 
> 物流供应链优化分析师，Power BI爱好者
> 
> 知乎：Beethovenist
> 
> LinkedIn主页：https://www.linkedin.com/in/jackson-lu-wen-jie-ba943224/

针对不同用户的数据查看权限，设置行级别安全性 (RLS) 是 Power BI 报告在企业应用场景下经常需要用到的特性；在去年 2 月份迭代中也增加了列级别安全性 (OLS) 的功能，可以借助外部插件 Tabular Editor 进行编辑，参考官方文档：

https://powerbi.microsoft.com/zh-cn/blog/object-level-security-ols-now-available-for-public-preview-in-power-bi-premium/

可是在实际应用中，如果用户对某些数据源的字段没有访问权限，那么就无法正常浏览报表中引用到相关数据的视觉对象，类似这样的报错：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMeg9FQboMiamcXVfzQzGhDmFPfCicvUGBaIX0fz3uLPbD3YJZ79DOIBSCbJYL2U54oDzmKgK6rg5xA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上述方式虽然实现了列级别的数据安全性，但从用户体验角度实在说不上友好，并且视觉对象中一旦出现无浏览权限的数据，所有计算指标就都无法显示，不够灵活。

最近新增的字段参数这一重要功能可以克服上述问题，接下来以一个实例来看下如何实现~

以PowerBI星球的案例数据做个简单的模型如下，由产品维度表和订单事实表构成：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMeg9FQboMiamcXVfzQzGhDmv4kDlQHcnY7vfKOTEichaP08zAP834Il7s3qImlA4ibp3HCQu5rHia9Sw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以收入、毛利度量值和产品维度表的产品名称新建[字段参数](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080273&idx=1&sn=b985ea8a53854f41a1ba75c0585cb3cd&chksm=8e13a446b9642d5085b1590f38ca7dd36c085269ae2d5d0fe75e09c57fc1ae270158d15d79db&scene=21#wechat_redirect)：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMeg9FQboMiamcXVfzQzGhDm2euUxAoFkkYGJO1iaIGmyOygibOoLAicID6LvRVCH08KO1YlDJaIEGIsg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

字段参数功能的具体用法请参考：[Power BI字段参数介绍以及常见应用场景](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080273&idx=1&sn=b985ea8a53854f41a1ba75c0585cb3cd&chksm=8e13a446b9642d5085b1590f38ca7dd36c085269ae2d5d0fe75e09c57fc1ae270158d15d79db&scene=21#wechat_redirect)

收入和毛利的度量值公式引用字段均来自事实表：

> 毛利 = SUM ( '订单'\[毛利\] )
> 
> 收入 = SUM ( '订单'\[销售额\] )

新建完成的字段参数表及其 DAX 公式代码：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMeg9FQboMiamcXVfzQzGhDmd3EPo66yUoP8cyAZEM4aL2azGbaPPoiahvaXYmMiahs61Oe8iboe510lA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMeg9FQboMiamcXVfzQzGhDmmSickJZyiaPS7bj91BUrnJ9eYNHSPUSBjfMibXyLxUMVojfe5srqpkmqQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

新建表格视觉对象，用字段参数表的可见字段作为列即可展示相关数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMeg9FQboMiamcXVfzQzGhDmmnfZOJJ4eUZfjvsxUP6jBKiaHCiacj7Tg6XDDNrxg8D3gOggNEibdRaUQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

此时再参考行级别安全性的设置方式（参考：[利用Power BI行级安全性，限制用户访问权限](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076638&idx=1&sn=04e90c833a99f5a0e9b2baa06b5c4a8e&chksm=8e13aa89b964239f010a579a4bfdb74ce2dd483b7d333d4a797ca03c12752ab75c1a0fa4e05e&scene=21#wechat_redirect)），新建一个 Guest 角色，并结合字段参数表限制该角色不能方位字段参数表的“收入”数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMeg9FQboMiamcXVfzQzGhDmjaPCicYrSMiaEdOuww8luLVmovLcDquoGu2pMuf2MHCiaYqCSnqLtOGQQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中 DAX 表达式为 ：

> \[字段参数\] = "产品名称" || \[字段参数\] = "收入"

回到报表页，选择以 Guest 的角色预览数据，此时表格中的收入一列就消失了，但是产品名称和收入数据依旧可见:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMeg9FQboMiamcXVfzQzGhDmg4dK5ltalAA3iaaHmia4bOVOzxSzk0Rl3MqAQJuR2MHickx5GOsicqEQjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

至此，利用字段参数功能生成的表，结合行级别安全性的设置，就十分灵活地实现了列级别安全性功能，用户也感知不到报表层面的报错信息，相比原生的 OLS 更为友好。

不过，这样的方法也有其代价，当报表的数据量比较大，会耗费较多的计算时间；本案例的列级别安全性条件较为简单，实际使用场景中会存在各种字段交替组合的情形，此时在设置角色权限时的 DAX 代码也相应变得复杂，部署使用前需要斟酌方案的灵活度、维护成本和用户体验。

参考文章：https://blog.crossjoin.co.uk/tag/row-level-security/

数据来源：后台发送关键字“PowerBI星球案例数据”获取
