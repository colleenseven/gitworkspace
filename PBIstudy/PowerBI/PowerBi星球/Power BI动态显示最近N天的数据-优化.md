---
create_date: 2021-05-20T19:58:19 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI动态显示最近N天的数据-优化
source: https://mp.weixin.qq.com/s/LIRctT96hqdrM_pky2JdYw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

之前发过一篇[如何利用PowerBI动态显示最近N天](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070920&idx=1&sn=2caa30a3ee4eb0f642d1fdc748f08f3e&chksm=8e0c40dfb97bc9c9011a46addf9900c69523e440a3bdbe676affce6bfd90e0a405affe8c0362&scene=21#wechat_redirect)的文章，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOKBEQ5iapShHdnIF2hKZBMP7zzUwXFlAx4xtKghPrX0tFCHd0ycI8G7E5tnicCuSmcupF53Cb7xWAQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

它的设计思路是，利用一个独立日期表生成切片器，来间接控制最近的N天，度量值只在最近N天时返回数据，最终实现的效果就是上面的柱形图只显示最近N天的柱子。

但是这种做法有一个弊端，就是由于独立的日期表与其他表没有建立关系，所以生成的切片器也只能控制这一个图表，当报表中还有其他可视化对象时，无法控制其他图表，导致在报告中不得不放置两个日期切片器。  

那么如何让这个日期切片器可以作为一个正常的日期切片器，不仅控制最近N天，同时也能控制报告上的其他图表呢？

我们这里变换个思路，和日期表相关的模型依然还是这样，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPsudSwFgK5pvrriaPw66ChfAfCY6gkLRmbVgV9qCjxWCPLJxibO8ro235mUGXBFiaJcLZg4N4khllUQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

但是与之前不同的是，**生成切片器的日期用模型中建立关系的正常日期表，而做柱形图时，坐标轴的日期，用未建立关系的独立日期表来生成。**

因为订单表与独立日期表未建立关系，如果还用原来的度量值，柱形图将无法正确显示，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPsudSwFgK5pvrriaPw66ChfK9dsicswTo0riae8M5Nl1KrlS29To9G8NTAickjRlrNlbt838582mCF4w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为独立日期表与订单表没有筛选关系，所以数据都一样。

那么如何解决这个问题呢？

解决它的办法就是修改度量值，让没有建立关系的表也能产生筛选作用，可以用TREATAS函数来建立虚拟关系，更改度量值如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPsudSwFgK5pvrriaPw66Chf6khSWwHdCGFbVUWYTNSMOdo6iacPjBnibkXv8GgXbQHFcVgNgZQrqiadg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

逻辑和之前的一样，只是这里用TREATAS函数，将独立日期表，视同正常的日期表来使用，然后用这个优化的度量值来做柱形图，就能得到和之前一样的效果了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPsudSwFgK5pvrriaPw66ChfG7X8canibvkM0mJPCteTNaRBoxTDicA0gACUtWfKtrx4Zz0KeF4QDtdA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当然这个日期切片器是建立关系的正常日期表中的日期生成的，同样可以控制该页面的其他图表，建议大家使用这种方式来设计类似的动态展现需求。

___

**温馨提示：**

第四届PowerBI可视化大赛火热进行中，访问PowerBI社区官网即可报名和上传作品：

http://www.chinapowerbi.com

**5月26日截止**，还剩不到一周的时间了，大家不要错过了哦~

___

[**新书上市**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
