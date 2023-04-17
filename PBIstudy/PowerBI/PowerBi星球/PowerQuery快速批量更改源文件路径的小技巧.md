---
create_date: 2021-04-09T20:05:03 (UTC +08:00)
tags:
aliases:
pagetitle: PowerQuery快速批量更改源文件路径的小技巧
source: https://mp.weixin.qq.com/s/vch52SWXB3R_cRpZjuZs0g
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

之前的文章中曾经分享过在PowerQuery中利用参数来动态切换源文件路径的方法：

[PowerQuery报错？利用参数轻松解决源文件路径问题](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073358&idx=1&sn=99e86bdde3a9831509fc8017890e0af8&chksm=8e0c5959b97bd04f4023fe469acc7774bf8307856086b58133d10b61bf518970b4fa7fbbdfe7&scene=21#wechat_redirect)  

在该文中，参数建好以后，是手动一个个调整每个查询中的M代码来实现的，显得比较繁琐，如果查询很多，这样操作效率也太低了，最近找到一个更简便的方法，这里再来介绍一下。

___

如果在一个分析报表中，有多个表格，在PowerQuery编辑器中对应有多个查询，是同一个数据源，但是由于数据源路径变更，需要调整每个查询中的路径地址，比如之前源文件在C盘，现在源文件必须存放在D盘，这样的话，PowerQuery中的各个查询将会报错，无法刷新。

先按照改[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073358&idx=1&sn=99e86bdde3a9831509fc8017890e0af8&chksm=8e0c5959b97bd04f4023fe469acc7774bf8307856086b58133d10b61bf518970b4fa7fbbdfe7&scene=21#wechat_redirect)的做法，第一步建立路径参数，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOricd1h0bOGt0a7mia0dwS8F1QsqI9Jrnjj1o6HLQFxheAvbDxQuq4AQhp1tR6KzlkIPeiaicibYbMJzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后第二步无需按照[该文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073358&idx=1&sn=99e86bdde3a9831509fc8017890e0af8&chksm=8e0c5959b97bd04f4023fe469acc7774bf8307856086b58133d10b61bf518970b4fa7fbbdfe7&scene=21#wechat_redirect)的做法，手动调整每个查询的路径代码，而是转到“数据源设置”，如下图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOricd1h0bOGt0a7mia0dwS8FbR8vgXj5WYn4Cq5icwibKK49DwMD2uEPau3bU8rVraN8Z8ZYDN0dIw0Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下面是操作步骤：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOricd1h0bOGt0a7mia0dwS8F36oUqTCFZ4ibnibAzWR6gTsAYSrvIx3o2zWkKNGpeOJVdvbibdpIYvDJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 在数据源设置窗口，点击左下角的“更改源”

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOricd1h0bOGt0a7mia0dwS8F32Fr9DcEadkZw26NPRfhXLbX6L3O6jFtDxdhTUPX1t1OQrTxC8xP5Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 文件路径左侧的下拉箭头，选择"参数"

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOricd1h0bOGt0a7mia0dwS8Fm9OBtOgtgA4TicCsbPjTrxKZeyicdavRwejU0KEfI9beZ927q6o9TAbw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 选择建立的路径参数（如果只有一个参数，默认就是这个）

然后点击确定，所有的查询的路径就一次性全部变更过来，而不再报错了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOricd1h0bOGt0a7mia0dwS8FQUjA7QtXH4rWrUEC7uNWicxe4Bica1PMJ7LoxqgiaUxqE87QHibuNO6l3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点开任意一个查询的高级编辑器，可以看到原来的绝对路径地址已经自动变更为参数了，和之前手动设置的一模一样。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOricd1h0bOGt0a7mia0dwS8FRxa8qmubybxw49D0icZBmm9oRNfuD0gMVymUtD0FmxllfrqS4MialDAg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常方便。  

如果你的数据源路径经常需要变更，不妨试试这种方法，当然你也可以不利用参数，每次直接在数据源设置中调整绝对路径地址。

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
