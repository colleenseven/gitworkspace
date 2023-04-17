---
create_date: 2021-06-29T19:49:21 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI可视化技巧：折线图上直接显示类别
source: https://mp.weixin.qq.com/s/yrsosoaz_9ubh6YAqpw3ow
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

制作多系列折线图的时候，需要使用图例来标识每个系列的名称，就像这样的折线图，国家名称作为图例，展示了多个国家的GDP的增长趋势，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOcsb41K0Fat6Uz0ekXIbWoLkibqZKoia6fId8bnvibP6pYOqXtNEpV1dLmw46gnibFW1r3sHCkatOu6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

根据折线图的设置，图例只能显示在折线图的周围单独显示，能不能取代这样的图例，直接将名称显示在折线上呢？

正常在折线图的各项设置中是没法做到的，不过利用计算组，这种效果也可以实现，和之前介绍的用计算组来显示最高最低点标签的思路一样（参考：[利用PowerBI计算组，设计个性化数据标签](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076121&idx=1&sn=505f2d704bb46b641d21900a1fa9c3f6&chksm=8e0c548eb97bdd985786642ae697183cda036d6418757981aea2a380921a78b2af3d59b6cc7a&scene=21#wechat_redirect)）。  

以上图为例，数据很简单，只有一张表，三个字段，年度、国家名称和GDP数据，做一个多系列的折线图，然后用计算组来实现上述需求。

创建计算组的具体的步骤不再详细介绍，主要是设置计算项的格式表达式，如下：

```
VAR maxyear_=MAXX ( ALLSELECTED( 'Data'[YEAR] ), 'Data'[YEAR] )
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOcsb41K0Fat6Uz0ekXIbWoozWCibDc2NH4N9zNeEVMCgiaGTtU5DEmsibJVcnBQvic6ojDB8M4LGP14w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后利用这个计算项生成切片器并选中，打开折线图的数据标签，就能得到下图的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOcsb41K0Fat6Uz0ekXIbWomYg6iaFKqrsfbNjiaRKvUmJP66eL62uc3PoYwfwJKWg7BxYaYW0BE1RQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

更进一步的，结合之前的动态折线图的案例（参考：[带播放轴的折线图，你可以这样做](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068920&idx=1&sn=151827fe4909c1f6501cdbd29046dcef&chksm=8e0c48efb97bc1f9c6cc142a36ab32fafc753d63535cf028d81767516afa60cf680275d28861&scene=21#wechat_redirect)），还可以随着折线图的播放，始终在折线头部显示该类别的名称。

以带播放轴的折线图为例，在计算组中增加一个计算项，设置格式表达式为：

```
VAR year_= SELECTEDVALUE('播放轴'[年度])
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOcsb41K0Fat6Uz0ekXIbWocNC1oZ7HgJtCaBfFsScvcfaXCwrHaqKHibBW8hnkOxrIgDM13AeBibeg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击利用Play axis制作的播放控件按钮，这个折线图就可以做成这样的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOcsb41K0Fat6Uz0ekXIbWoDvvxN8voQ8Old6po4CvPtMVHMPY3WG3Hic0fW39UibgSbJyG6McLXEicg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

关于计算组的更多介绍和应用，请参考：

[PowerBI发布重磅更新，一文带你熟悉计算组怎么用](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072054&idx=1&sn=d403fdef264cbfb6fca46d33bd0083b9&chksm=8e0c44a1b97bcdb7fe466afe90d0f3d4b86738a0da7241f9125d4f36a1fcbd89c094b7ea42d8&scene=21#wechat_redirect)  

[PowerBI设计技巧：动态数据格式](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074205&idx=1&sn=d8c9d1a3f80245e6e3b1f5bd2d14a053&chksm=8e0c5c0ab97bd51c1cdcc44737ff0967f5179b716c5f0bc90c87abcd977153b10cd11cdc3219&scene=21#wechat_redirect)  

[利用PowerBI计算组，设计个性化数据标签](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076121&idx=1&sn=505f2d704bb46b641d21900a1fa9c3f6&chksm=8e0c548eb97bdd985786642ae697183cda036d6418757981aea2a380921a78b2af3d59b6cc7a&scene=21#wechat_redirect)  

[利用Power BI计算组，动态切换各种范围的数据标签](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076142&idx=1&sn=f04ec3ffaf62198b9b993de357ba4ee7&chksm=8e0c54b9b97bddaf185ba5aa55418d0b9b780160261179d43bf41ec1cec5aa7114e94332f99a&scene=21#wechat_redirect)  

___

**[新书上市：PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

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
