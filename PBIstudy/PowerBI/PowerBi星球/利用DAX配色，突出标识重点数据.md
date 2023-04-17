---
create_date: 2021-04-29T20:02:14 (UTC +08:00)
tags:
aliases:
pagetitle: 利用DAX配色，突出标识重点数据
source: https://mp.weixin.qq.com/s/HsE-h7XIRFY0Ox6SypG2HA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

正常的图表颜色一般是统一的，如果需要重点关注部分数据，可以将它们用不同的颜色标记出来，比如每个产品的收入对比柱形图，对于特别关注的产品突出显示。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP1o3OMmwFH6IKmf0ooaBcZpMZTDgqekelpqvlGpJPNy0dcb6SK54Nvz7cJde5OogHUI6G2hPeZEA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在Excel中可以轻松对某个柱子标记为不同的颜色，PowerBI也可以单独调整某个柱子的颜色。

但是如果需要标注的产品是随着时间动态变化的，可能就不是那么容易做到了。  

以上面的柱形图为例，假如每年关注的重点产品是不一样的，数据如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPWGFI1Ths7KnKv7YJ77Dib6f01j4QwsR8iaYKwVrx7Qk4Ku0ZCZjcwKaMibqT3hmNMER6f6URicvjXMQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如何在不同的年度，突出显示不同的产品呢？  

其实利用一个度量值即可实现：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPWGFI1Ths7KnKv7YJ77Dib6uJzNqY9dVrrOPzNaicaVQHQ7jnjgicw9gT9OibPTo9svck6xoYa5koYEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在度量值中已经批注了主要了逻辑，其中最重要的是利用LOOKUPVALUE函数，查找当前上下文的年度和产品，是否在"重点产品表"有相应的记录，如果有记录，颜色调整为"orange"。

并且这个函数不需要两个表建立关系，所以这个重点产品表可以是独立的，不用对原模型进行任何修改。  

然后打开柱形图的颜色设置，点击fx，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP1o3OMmwFH6IKmf0ooaBcZVwOospWpAHJccRRWpoWM6d2MCROYhDsYoRZTOS61Sh0R2vQN3o4Vpg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在弹出的窗口中，选择按"字段值"模式,并选择上面建好的度量值，即可实现动态对重点产品配色的效果（参考：[利用这个新功能，轻松实现图表的动态配色](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068328&idx=1&sn=481bc433696f3569ed6d1c0bb5f80556&chksm=8e0c753fb97bfc2948e857568b33fc553da3d3449d7825e1651612de4529a532ed32d17ea7d3&scene=21#wechat_redirect)）

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPWGFI1Ths7KnKv7YJ77Dib6dtOnqDwvNnnSNFYvvglnrbeBS6bmibenB1djMK0cspicQtHFs8k64bzA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

是不是很简单。

在不更改原有数据模型的情况下，仅仅是利用一个辅助表和一个辅助的配色度量值，就实现了突出颜色显示的效果。

___

[**新书上市**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
