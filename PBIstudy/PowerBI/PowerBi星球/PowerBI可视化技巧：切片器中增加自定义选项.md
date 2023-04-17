---
create_date: 2021-04-14T20:03:55 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI可视化技巧：切片器中增加"自定义"选项
source: https://mp.weixin.qq.com/s/21CHlw-0l6d08kwbrUVkmA
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

以前的文章中曾分享过利用切片器来动态切换最近7日、最近30日的文章：

[PowerBI设计技巧：动态切换昨日、最近7日……](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071645&idx=1&sn=23011efad1a97881bafd8c4b4eacb254&chksm=8e0c460ab97bcf1cc90e4f1814dbc40668f2fc6f50cb6620cc8ed228a812311807b2c295a6ff&scene=21#wechat_redirect)  

这个可视化交互效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJM69NZApWpMfWwNqLWX5pKABynS96I20fXf1JIy1ld6KuY3aKrMUbhb4nSVtiaFzYAMy4yA4rMee7Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

最近碰到星友的提问，大概意思是，如何能够在此基础上，增加一个自定义的选项，除了能够选择最近7日、最近30日等固定的期间，还能够让用户自由选择其他的任意区间，能不能实现呢？  

在PowerBI中通过一定的技巧当然是可以做到的，我通过在原有的切片器中增加一个选项“自定义”，并在页面上添加一个正常的日期切片器，当选择自定义时，日期切片器启用，可以正常选择某个区间，可视化效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOYkvZXqSpIQbdhZRCzKwOqKNtKrGlTcb3sxIpCbGDcnBx2QTDSO803nLxjKBPr6xmmUBT9HdLDiaA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这是怎么做的呢，下面介绍一下步骤，这是在[上面文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071645&idx=1&sn=23011efad1a97881bafd8c4b4eacb254&chksm=8e0c460ab97bcf1cc90e4f1814dbc40668f2fc6f50cb6620cc8ed228a812311807b2c295a6ff&scene=21#wechat_redirect)的基础上改进的，如果你还不清楚不加自定义时的效果是怎么做的，建议先看看[那篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071645&idx=1&sn=23011efad1a97881bafd8c4b4eacb254&chksm=8e0c460ab97bcf1cc90e4f1814dbc40668f2fc6f50cb6620cc8ed228a812311807b2c295a6ff&scene=21#wechat_redirect)。  

**1\. 增加自定义选项**

只要在历史维度表中增加一个自定义的值就可以了，至于自定义对应的天数，无所谓，随便写个数字都行，该数据没有实际用处。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYkvZXqSpIQbdhZRCzKwOqEemu9Nv6n2cIUPqdOV6lt9tMFYyHYHOChqibgbmlntLTptWuMVKEaXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

增加自定义后的切片器样式：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYkvZXqSpIQbdhZRCzKwOqjDO94icOJErIm3EPiccCRSmCLNSry94H9qichdfONWxjZoibJLUbLHZicrA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. 添加一个日期切片器。**

正常使用日期表中的日期列，生成一个切片器放到画布上就可以了。  

**3\. 自定义设置切片器**

这一步最重要，为了在用户选择其他选项时，让切片器不起作用，可以写一个度量值：

> 日期切片器激活 =
> 
> IF(SELECTEDVALUE('历史维度表'\[维度\]) ="自定义",1,0)

然后把这个度量值放到日期切片器的筛选器中，设置为等于1：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYkvZXqSpIQbdhZRCzKwOq3SzpKicSEpKHCOdGyvPJibiardAYibrC3gT9sT5oGa4kaicBG9ZQQd1iaIWw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并编辑交互，让自定义选项所在的切片器可以筛选日期切片器，就可以达到只有点击“自定义”，日期切片器才能使用的效果了。  

为了让日期切片器的可用状态更加明显，还可以自定义标题和颜色，来提示用户如何使用：

> 日期切片器标题 \=
> 
> IF(
> 
> SELECTEDVALUE('历史维度表'\[维度\]) ="自定义",
> 
> "请选择日期区间",
> 
> "自定义区间不可用！"
> 
> )

> 日期切片器标题颜色 =
> 
> IF(
> 
> SELECTEDVALUE('历史维度表'\[维度\]) ="自定义",
> 
> "#E79B25",
> 
> "#91AFC8"
> 
> )

将这两个度量值添加到切片器的标题设置中：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOYkvZXqSpIQbdhZRCzKwOqUzCMcr4nmpV179suxxrc0tzO0wpssKiaMJswM33nAD24QofqD09KRRQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就能达到下面的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOYkvZXqSpIQbdhZRCzKwOqF1viappQzuMCmMByg7AvZBYiaUYsqUwuBMF1xUzPNlqTEzIX83JNuqicg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样就能更方便的让用户进行各种自定义交互了，掌握了这种技巧以后，当遇到这个需求时，其他类型的切片器也可以尝试制作自定义选项。

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
