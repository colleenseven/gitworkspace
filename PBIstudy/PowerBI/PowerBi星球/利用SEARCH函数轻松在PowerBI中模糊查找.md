---
create_date: 2021-04-06T20:05:31 (UTC +08:00)
tags:
aliases:
pagetitle: 利用SEARCH函数轻松在PowerBI中模糊查找
source: https://mp.weixin.qq.com/s/3yMplwq-Ws9CzK4znw_lPw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

不少人问过如何利用DAX进行模糊查找，其实挺简单，熟悉一个函数就可以了，它就是SEARCH。

SEARCH函数的功能与Excel中的类似，就是查找字符所处的位置，用法很简单，在DAX中的语法如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPNSXc1CgoGZBld5oymroazo7FqfJOrzHUGMxqBRlTENxTsIgLILXwV9TX4jiaKu620AhHULjDsUrQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

查找文本位置这个原始功能使用场景不多，更常用的是结合FILTER函数进行模糊匹配，假如有下面这个数据，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPNSXc1CgoGZBld5oymroaz8jHaGkDGMAFVDKaYibicLqtAVq5Zp8dQMNHia8dvXhCdODpFZrqq3qdfg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**如何从这些长尾关键词的搜索数据中，找到包含“数据分析”的搜索量有多少？**就可以利用SEARCH函数来解决。

直接写一个度量值:  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPNSXc1CgoGZBld5oymroazjNlODGSfA9hnvYuicucicbWR4E0WBIDmJ8oZ92SbRog9AY8PwZHLrCTw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个度量值的逻辑是逐行迭代数据表中的长尾词，把包含“数据分析”的行筛选出来，然后汇总计算出搜索量累计。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM1yMJ0ZtLMSytF3IIBXIpHRHdCGEVKwBkDVTbnNaSngcCIgDC5UnX2u0x4ibGOMLDDict5lRBAVx4A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想同时包含两个关键字的搜索量，还可以利用通配符来完成，SEARCH函数支持通配符，可以在第一个参数中使用通配符。

通配符的含义与Excel中一样，问号(?)表示任意单个字符的匹配；星号(\*)表示匹配任何个字符。如果要查找实际的问号或星号，可以在字符前键入转义符波浪号(〜)。

比如想计算包含“上海”和“数据分析”的搜索量，度量值可以这样写：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPNSXc1CgoGZBld5oymroazyP1CavU5JiaMl0sbpV4Icz2ibHhtDvyyFOrwW3azLnSCAQnfEW6JiccYA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当然，它不仅仅只能搜索一个关键词，如果有个关键词列表，比如下面这个：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPNSXc1CgoGZBld5oymroazDBbU2Fhoqto02g3cFkiaTkPv7qDJc17QPGSaTqjibN7DgRfgJwDogElg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

要想得到每个关键词的搜索量，度量值这样写就可以了：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPNSXc1CgoGZBld5oymroazcxyIJbfyf9sDGHaaJz81YlWq7iaicI7HeaiaJlhNLwr2fsa8mOYv2LE1g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后利用关键词字段和上面这个度量值制作矩阵，结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPNSXc1CgoGZBld5oymroazz0jILj9XBX2Zdve2siawSNxQ3QBH9mytrZmRq9icEJfJ6o4ukdQZPsKw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是挺简单。

注意SEARCH函数与FIND函数的区别，这两个函数非常相似，FIND不支持通配符，并且区分大小写，如果你需要严格区分大小写进行匹配查找，请使用FIND函数，其他情况都可以使用SEARCH函数，SEARCH的应用范围更广。

___

[我的新书已上市](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)，帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPNSXc1CgoGZBld5oymroazzO20buWRlnYfhdU1R1Ona2NXtshZzwmgdQXjZ8QqYxUicSXNUNqkSNA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
