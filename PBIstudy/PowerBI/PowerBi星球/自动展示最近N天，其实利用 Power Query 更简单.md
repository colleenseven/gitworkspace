---
create_date: 2021-03-04T20:14:57 (UTC +08:00)
tags:
aliases:
pagetitle: 自动展示最近N天，其实利用 Power Query 更简单
source: https://mp.weixin.qq.com/s/MUx3JFhvV0EENGmzJ0ViDg
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

最近发生的业务往往需要更及时的关注，所以报告中经常有展示最近N天数据的需求，之前曾介绍过利用DAX动态的显示最近N天：

[Power BI动态显示最近N天的数据](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070920&idx=1&sn=2caa30a3ee4eb0f642d1fdc748f08f3e&chksm=8e0c40dfb97bc9c9011a46addf9900c69523e440a3bdbe676affce6bfd90e0a405affe8c0362&scene=21#wechat_redirect)  

如果在报告中只需要分析最近N天的数据，其实也可以不用这么麻烦，还可以利用PowerQuery的日期筛选器，更方便的实现。  

数据导入到PowerQuery后，按数据中的日期字段来筛选数据。比如这个订单表，只需要点击订单日期列右侧的下拉箭头，即可找到日期筛选器：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3tIibqTd9ct9sO7DE8JGNTwkMyjy4XhSnq8sTS3XLtE4kPghicdbkkIvpuJJNK5ANWvfPc6xibqo9Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在日期筛选器中内置有各种粒度的筛选，比如昨天、今天、本周、上周、本月、本年等等，甚至也可以细化到按小时、分钟、秒来筛选行，还可以自定义筛选。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO3tIibqTd9ct9sO7DE8JGNTkMd8Wg4rpNgvTHg80BvAo6z8icRtt1hyib7LiaibW9sBkTvaId9aOb26WQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

如果仅需要最近5天的订单数据，只需要选择“在之前的”，然后在弹出的窗口中输入5天就可以了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3tIibqTd9ct9sO7DE8JGNTgTkEXqEpXowqHIlsqIDu3RtrYUJRSjqsZGuKURZ2Q97lZUUHa3qnGQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后上载，模型中就是最近5天的数据，直接做可视化展示即可。

___

上面用的之前5天不包括今天，如果想要包含今天的最近5天数据，可以这样设置：之前的4天以及今天。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3tIibqTd9ct9sO7DE8JGNTWuib9j3TswJT645UAqC6naqurIfAp7qmaQfIGY9V0HP7EAPnVd0iav5Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

如果打算修改为最近15天的数据，点击“转换数据”进入PowerQuery编辑器，点击筛选行这个步骤旁边的小齿轮，可以再次进入筛选行的按钮，将5修改为15就可以了。

也可以直接修改这个步骤的M代码，将其中的5改为15：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3tIibqTd9ct9sO7DE8JGNT90S7M2qmD6BkOvdJ6aeIvX8ZSHVVJM3KNHicPIibNG11zaLs0JPpaSWw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还可以利用PowerQuery的参数，将这个最近N天动态化，先在PowerQuery里建个参数：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3tIibqTd9ct9sO7DE8JGNTvAvxE2qhXxwuEnA3LOZiaRwAicib15crZnxiab63Hl66CMBSKBVnThwNRg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后修改M代码为：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO3tIibqTd9ct9sO7DE8JGNTKchUX8MrrUY2MtdLbBfLic1tLHm9TPrNSXuY8sOISpnCv85QueDnwHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就可以根据参数的值来动态的筛选最近N天了。

这种做法加载到模型中的数据永远就是最近N天的，会随着日期的变化而动态变化，更加简单轻巧，但简单也伴随着单调，它无法灵活的根据用户交互来展示某个日期之前的最近N天，也无法仅利用这张表做其他的分析，比如同期对比分析等。

具体用哪种方式，如何建立模型，依然是根据实际业务的需要来衡量。

当然如果你的历史数据非常多，而你只需要分析最近3年的，同样可以利用日期筛选器来动态的提取最近3年的数据，而无需将全部历史数据都加载到数据模型中，这样可以显著的提升模型性能。

关于PowerQuery日期筛选器，其他的粒度和筛选方式可以自己尝试一下。

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
