---
create_date: 2021-07-29T18:16:50 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI报告设计技巧：一键部分重置
source: https://mp.weixin.qq.com/s/ExCjIzbaL20aeFXY7K4JcA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

[之前](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073105&idx=1&sn=630078447d92ab54c9c049fb8a656953&chksm=8e0c5846b97bd150bd23d3af28b62bf9813d17b339a2a4199096cdb076fd664b0e744d2808b8&scene=21#wechat_redirect)介绍过如何一键重置报告中所有筛选器的技巧，无论切片器选择什么类别，都可以一键返回到初始状态：

[PowerBI报告设计技巧：一键重置](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073105&idx=1&sn=630078447d92ab54c9c049fb8a656953&chksm=8e0c5846b97bd150bd23d3af28b62bf9813d17b339a2a4199096cdb076fd664b0e744d2808b8&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPrC4YSlkeGfjCZhAY28LLXS249aKsHV0f0WluVbJxThFp3c1yARjpwk4Eia3TbmFWyJicjXEibrSib4A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

在这个示例中，有三个切片器：公司名称、年度和报告类型，利用书签，可以一键重置到 "万科2019年度报告"数据的状态。

**但实际应用时，或许并不需要全部重置，而是重置部分切片器，比如无论选择哪个公司，都重置到该公司最新一年的年度报告，也就是"2019年年度报告"，公司名称不需要重置，这种效果是否可以实现呢？**  

利用书签，同样可以实现部分重置，依然以这个财务分析报告为例，下面来看看如何操作的。

**1\. 添加书签**

为了让书签保存最新一期年度报告的状态，年度切片器和类型切片中分别选中2019年、年度报告，然后按住Ctrl同时选中这两个切片器，添加书签：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOv6BFljRicgjwae3yXNIVh9OuPdrhcV1mqbMwoFmmZZLOMyzTic7YZ66eh1YGU62WJMBAwfDDMz15g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

书签可以命名为：最新年度报告。  

**2\. 设置书签属性**

右键或者点击书签右侧的三个点，设置书签的属性，勾选“所选的视觉对象”，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOv6BFljRicgjwae3yXNIVh9IEuW65zvHJI3sO6PMBz3exagEBdR26vkFicGvZedlNp1EMNhQHVMmMg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并且这里的“数据”属性一定不能去掉勾选哦。

**3\. 添加按钮**

在页面中插入一个按钮，并设置该按钮的操作属性为上面的书签，制作完成，来看一下效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOv6BFljRicgjwae3yXNIVh99VSibGzDjH4ZR5fDfjFzudaBqvWNqtg8zYCcHDPHMu8mwsaLAE1oibPQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样就实现了，无论选择哪个公司，都重置到该公司2019年的年度报告数据。  

上面设置的书签属性，你也许还注意到了，我把“当前页”的勾选也去掉了，它的效果是，**书签只保存页面的状态，但是不跳转到该页面**。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOv6BFljRicgjwae3yXNIVh9Wp6AeMHJKV3moagb6hXb3nUdfhb9HibibPU1ZEEeTnxk8cUIxaGF1vqQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

比如上面设置的书签是在资产负债表页添加的，当我在利润表页点击按钮时，返回的是利润表的最新年度报告数据，而不再跳转到资产负债表：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOv6BFljRicgjwae3yXNIVh9pTf5oYgZoIWOLJsp5lyIico3rxw3RQ8DfALNibiaZeFtLQomG8G0yWRvA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样的交互是不是更加自然呢。  

这里灵活运用了书签的"数据"、"所选视觉对象"和"当前页"属性，大家应该准确理解书签每个属性的作用，以便来设计更具体更精准的交互需求。

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
