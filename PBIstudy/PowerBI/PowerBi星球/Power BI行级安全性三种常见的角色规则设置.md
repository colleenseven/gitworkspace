---
create_date: 2021-07-22T19:43:31 (UTC +08:00)
tags:
aliases:
pagetitle: Power BI行级安全性三种常见的角色规则设置
source: https://mp.weixin.qq.com/s/X27jbJFtAoOutYG82p1JTg
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076638&idx=1&sn=04e90c833a99f5a0e9b2baa06b5c4a8e&chksm=8e13aa89b964239f010a579a4bfdb74ce2dd483b7d333d4a797ca03c12752ab75c1a0fa4e05e&scene=21#wechat_redirect)介绍了[PowerBI行级安全性](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076638&idx=1&sn=04e90c833a99f5a0e9b2baa06b5c4a8e&chksm=8e13aa89b964239f010a579a4bfdb74ce2dd483b7d333d4a797ca03c12752ab75c1a0fa4e05e&scene=21#wechat_redirect)设置的一般步骤，本文再继续介绍一些常用的权限管理角色的设置。

仍然以下面这个PowerBI报表和业务人员张三为例，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPBO6wTjsAnvQrQtib8AqrRN3fmCUWGRw0PoJlNavX7I2kD876jKUvRGmuczOr65xW61TzEBRD8icxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

前面介绍的是张三负责上海地区的业务，下面根据他所负责的不同业务角色来设置规则。

**1\. 负责"上海市"和"南京市"的业务**

负责两个城市的业务，他就应该可以查看这两个城市的所有数据，规则可以这样设置：  

```
[客户城市] = "上海市" || [客户城市] = "南京市"
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOUnvRd32aPt2yxwD2oArMEtPhiahe5HjKWCZBCxoniaibvOFQqz71icAXwM2VsVGyO7IFK1LNnOdcnxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

他收到的报表效果就会有上海和南京两个城市的数据：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOUnvRd32aPt2yxwD2oArMEDnTYDiaibJez5LZJmFLvcAK8GH4icxaGuy3bo58wGpzkd4smmy62FEw2g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

行级安全性完整的设置步骤不再详细介绍，如不清楚参考[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076638&idx=1&sn=04e90c833a99f5a0e9b2baa06b5c4a8e&chksm=8e13aa89b964239f010a579a4bfdb74ce2dd483b7d333d4a797ca03c12752ab75c1a0fa4e05e&scene=21#wechat_redirect)，这里直接按这个规则预览该角色的效果，下同。

**2. 负责"上海市"的"耳机"业务**

可以对两个表进行设置规则：  

```
[客户城市] = "上海市"
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOUnvRd32aPt2yxwD2oArMEmuvBLolbqY3lo5mERozkCgPibt4wzZphMPLwDibW2fdRPwvaic3puMd4A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOUnvRd32aPt2yxwD2oArMEuTn1f9dqcL6j9lm9icbf9AZmLyoKgGrf5ITbRE5zQO0BV5QzoBtNHBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过这样的设置，他能查看的数据，就只有上海市的耳机业务数据，相当于两个规则的交集，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOUnvRd32aPt2yxwD2oArME2Vsjht2IzGQZwZpTeNPKALN3g4NprxxjjuFnwptjiaqJnxKBDzVPCHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3\. 负责"上海市"的业务和"耳机"的业务**

如果张三不仅负责上海市的业务，还负责全部的耳机业务，那么他能查看的数据就要包括所有上海的数据以及所有耳机的数据，相当于两个条件的并集。

这种情况可以创建两个角色：上海业务、耳机业务

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOUnvRd32aPt2yxwD2oArMEzkcoJBX2eSAfSdXekxNmhp426kvZiby6d3UDxpt4JWeHtgohqIzicxDA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOUnvRd32aPt2yxwD2oArMEnES9SeNOy23Epbe7ok7vgmIasjmaDPq15t7asutUjiaY0N88w0g2AicQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后这两个角色都把张三的账户添加进去，他就可以同时查看两个角色的数据，勾选两个角色来验证：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOUnvRd32aPt2yxwD2oArMESibczia8276o6MOfrKULWgorj6KzUjiceibPibRTroCx5WeCQxKtw1Vh5yw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOUnvRd32aPt2yxwD2oArMElOpZLaBiagubAHHGicPrJCdGuSD7nUeypMWn0YGdFA51yz7RMutAwicuQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上就是几种常见的角色设置，灵活运用以上思路，利用行级安全性精确控制特定人员查看数据的范围。

___

**[新书上市：PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

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
