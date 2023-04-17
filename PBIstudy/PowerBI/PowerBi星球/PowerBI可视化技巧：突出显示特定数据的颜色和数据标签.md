---
create_date: 2021-05-08T20:00:07 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI可视化技巧：突出显示特定数据的颜色和数据标签
source: https://mp.weixin.qq.com/s/83o6edjgbsHQT5ByrLGNlA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

[上一篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075726&idx=1&sn=b41ae73e73aea78aef622ee4064fc268&chksm=8e0c5619b97bdf0f7fddb7cd890b23e8b213d99b57853f37a7272e06a55d9cc0304710e8a15f&scene=21#wechat_redirect)只是介绍了如何突出显示颜色，如果需求不仅仅是突出显示颜色，还需要将重点数据的数据标签也显示出来，应该怎么做呢？

按[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075726&idx=1&sn=b41ae73e73aea78aef622ee4064fc268&chksm=8e0c5619b97bdf0f7fddb7cd890b23e8b213d99b57853f37a7272e06a55d9cc0304710e8a15f&scene=21#wechat_redirect)的做法，无法单独显示特殊数据的标签，所以这里我们换一种方式来实现。

依然是[上文](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075726&idx=1&sn=b41ae73e73aea78aef622ee4064fc268&chksm=8e0c5619b97bdf0f7fddb7cd890b23e8b213d99b57853f37a7272e06a55d9cc0304710e8a15f&scene=21#wechat_redirect)中用到的数据模型和重点产品表，下面来看看这种方式的操作步骤。

**1\. 建两个度量值**

将重点产品和非重点产品的收入分别写两个度量值，如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP1o3OMmwFH6IKmf0ooaBcZ7t8qcqhvAFuDJzdYussADUHneQCNyMBkLPGUEjhFicR7Dq2TZTWvuibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP1o3OMmwFH6IKmf0ooaBcZF9USVfxskusDibNclYy400amfyNFxl7SZeFGyBx96ibMjFmerCAY9yIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这两个度量值的逻辑类似，只是最后返回的结果，一个只返回重点产品的收入，另外一个只返回非重点产品的收入。

**2. 生成堆积柱形图**

利用上面两个度量值生成堆积柱形图，字段如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP1o3OMmwFH6IKmf0ooaBcZX5qm8l4aBsjibgVjoA4Hy0IgxIdlfPm02lgREibHO8RlTDfAbcvqyicxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3\. 调整数据颜色**

因为上面作图时用了两个度量值，图表中就有了两个系列的数据，对重点产品设置不同的颜色，在格式面板中直接调整就行了，无需按照度量值配色。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP1o3OMmwFH6IKmf0ooaBcZwyXXwGjic5MsZbibjLiaKculHic0FrBxffRItlYiaKtkvO0eEO9ibgibersNQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**4\. 显示数据标签**

打开数据标签，并利用自定义系列，显示"重点产品"的数据标签，关闭"非重点产品"的数据标签。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP1o3OMmwFH6IKmf0ooaBcZEIetbdyy6WibasicTSLHrm6x1b26yFUkIxduHFHeQPXm0r5YXwCYqSqg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就能实现突出显示重点产品的颜色和数据标签了，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJP1o3OMmwFH6IKmf0ooaBcZfhDWwJaTZLBAqlw7Zyb6UicYQAengSmO57euylibf7ZzuiceTCQCoz8RQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这个技巧，加上[之前文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484075726&idx=1&sn=b41ae73e73aea78aef622ee4064fc268&chksm=8e0c5619b97bdf0f7fddb7cd890b23e8b213d99b57853f37a7272e06a55d9cc0304710e8a15f&scene=21#wechat_redirect)中的方法，都是DAX作图的常用技巧，希望大家能够灵活运用，数量掌握，然后才能随心所欲的利用PowerBI设计个性化的数据展现。  

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
