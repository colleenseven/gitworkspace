---
create_date: 2020-09-12T20:38:57 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI报告设计技巧：一键重置
source: https://mp.weixin.qq.com/s/mpZyODWWh3ILywNAo9J_0A
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

今天周末，分享一个简单而实用的报告设计技巧：**报表数据的一键重置**。  

在一个报告中，一般都设计有众多的维度切片器，便于用户自行探索，但用户一番尝试之后，如果想回到报告最初的状态，却可能已经忘了最初的状态是什么样了，即使还记得，也需要手动一个个把切片器还原回去，费事费力。  

有没有更便捷的办法呢？

其实利用书签，即可一键还原到最初的状态。以财务分析报告为例，下面是操作步骤。  

**1、在初始状态添加书签。**

假如初始状态设置为万科的2019年度报告数据，在这个状态下，添加一个书签，可以重命名为“初始状态”。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPrC4YSlkeGfjCZhAY28LLXQ6lrx5F7E6gNCdzf4kzYI4qdUjuKyYLIp9WIc9ZeKrSMX1yGU0LGmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于书签的制作可以参考：[PowerBI中的书签，真的非常有用！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068219&idx=1&sn=b74e0d16ac61413a90fb5f7837dea112&chksm=8e0c75acb97bfcba745fe9ba7eb4ca2aa83d0af34a17668284170b97c68b2d3dc909dc9eb936&scene=21#wechat_redirect)

**2、在页面添加按钮。**

点击插入>按钮>重置，就可以在页面中添加一个按钮，可以拖动调整该按钮的大小和位置。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPrC4YSlkeGfjCZhAY28LLXSV6lHyHgNwKsUgLziaxkvcsLbNeHS5DcqtnYOsg6Szc7Cs3ueGzdc5Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当然，这里添加按钮并不是必须使用这个“重置”按钮，其实使用任意一个按钮都是可以的，甚至可以从本地导入一个图标作为按钮。

不过为了用户都能快速理解这个按钮的含义，降低沟通成本，建议使用内置的“重置”按钮。

**3、设置按钮的操作属性。**

选中第2步添加的按钮，在右侧的设置面板中，设置操作的属性，类型选择为书签，然后选择第1步创建的书签“初始状态”。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPrC4YSlkeGfjCZhAY28LLX4YW5rEOZb9cCJYc9tAiaHmD9TBHASGCsN5E8o0J0u8RJ5RhLhy0OO8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

至此这个重置按钮制作完成。

下面看看效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPrC4YSlkeGfjCZhAY28LLXS249aKsHV0f0WluVbJxThFp3c1yARjpwk4Eia3TbmFWyJicjXEibrSib4A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

无论年度、公司切换到哪个类别，只要点击“重置”按钮，即可一键还原到最初的万科2019年年度报告状态。  

这个一键重置的原理就是书签的数据锁定属性，右键"初始状态"书签，可以看到【数据】是勾选的，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPrC4YSlkeGfjCZhAY28LLX7uX6icEXsvtQNia25hzXcbbibO7pwP0iaqWsGdyiaBWpjxugTMW95jwWRJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

数据属性的含义是，创建书签时，是否将该页面当时的数据也包含进去。如果勾选，当跳转到这个书签时，这个页面依然回到当初创建书签时的页面数据。

并且这个属性是默认勾选的，如果你不想锁定这个数据，跳转后需要页面数据动态变化，就应该去掉【数据】属性的勾选，比如前面介绍下拉菜单的设计时，就是专门将这个属性的勾选去掉：

[Power BI导航设计：多级下拉菜单](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073016&idx=1&sn=e56715750245f317c8c9b11ced5130a1&chksm=8e0c58efb97bd1f99f93b7023a3753efc3e83ac04ed230f86c2bdc9785dc69991f3ba1401d25&scene=21#wechat_redirect)  

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和2.4k+ 学习者一起成长
