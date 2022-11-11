---
aliases: null
create_date: 2022-01-19T12:30:09 (UTC +08:00)
tags: 
pagetitle: Power BI可视化技巧：矩阵中迷你图的妙用
source: https://mp.weixin.qq.com/s/_5Q4pwqzHvcnSP9JwAlf0Q
author: 采悟
status: 未阅读
category: 
uid: 
---

本文介绍一个上个月新推出的矩阵迷你图功能的妙用。

平时在报告中显示指标数据的时候，不想仅仅用卡片图显示一个醒目的数字，还打算同时显示这个数据的趋势，这种显示方式，以前介绍过几种方法，比如下面这些：  

内置KPI图的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNvicLPyJFBhwgn9StX6Zh1eZGB7ficjoRqgYJb8ia1yysV3O6rqTZLZ9uKCsYdMfuwS7ibRAcDrCbYrA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参考：[KPI图](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067440&idx=1&sn=ba9f4e72478d3f6e6d021c00aea66b41&chksm=8e0c76a7b97bffb1d715a0e9307800078eff145cbc2ebfa3c9390737afa1ae57da65a1836ac2&scene=21#wechat_redirect)

自定义图表的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPZ7PBib8zibWKqdfFhzLWs4VqM8ZbKlQ1svk2ouFsVxICqvXJTUp0tFO5dFEJ21iaxRNO4q9CQqp0XA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参考：[Sparkline by Okviz](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072525&idx=1&sn=4357859fdad3c3f7046163e3669c61ad&chksm=8e0c5a9ab97bd38c9aee957c4a56beba70f31d4d52a66302606a2504303e6408fa5afd603706&scene=21#wechat_redirect)

现在还可以用矩阵来实现类似的效果。

假如在报告中展示每个产品的收入指标以及变动趋势，可以先做个简单的矩阵，将"产品名称"放到矩阵的【列】中，度量值"收入"放到【值】中，然后鼠标放到“收入”上右键：添加迷你图：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2NIfoiaMqTFnBykBKeicNxp3PnFCJ0vptzlFAhic4tBS9QmJOskhOK61ibGL4DavcBJBKDa1Jofcz0A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

迷你图的X轴字段可以选择日期表的“年度月份”：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2NIfoiaMqTFnBykBKeicNxpUUyzOYyD43NKXnDR5Hk5QhV37Y9bYqWJKgn8FfcNUBqibqcQZq67sNg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

就有了每个产品的收入趋势的迷你图：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2NIfoiaMqTFnBykBKeicNxp4yO72akIowXxKrJIVBiaCCicg0ILLiayBUpnuTqmdHTicicff8PQ0o57lNA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后打开矩阵的设置面板：值>选项，打开"将值切换到行":

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2NIfoiaMqTFnBykBKeicNxppGnOPh2x3jJ0ibEssskRoeTia5xT40JDYmWxfdAHG0pJIn2RLibLeUFibQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

就有了下面的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2NIfoiaMqTFnBykBKeicNxpLicuwWln78RgWp1K3rlDIpxE42blATibE7cibAWibSJmV9Eb17ARNgcPIw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

将左侧的标题行隐藏起来，去掉边框和背景色等细节的设置、为迷你图添加最高最低点标记（关于迷你图的设置，可以参考：[PowerBI 2021年12月更新，你应该知道的几个变化](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078544&idx=1&sn=4bbafb99f595a3e0785f394a7de5af0b&chksm=8e13ad07b9642411cd6c08f281ece6f6c6120a9ab6b2cef62ff0bd4fa1363a57bf81be3da342&scene=21#wechat_redirect)），就可以得到下面的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2NIfoiaMqTFnBykBKeicNxpRd95U1hInBWUmkrqLbWEUtXXVEmnH8rfrCvdVpFmtj9ZJA5g6LYWJw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果添加一个切片器来切换产品，并为矩阵添加一个边框，就可以只显示某一个产品的指标：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2NIfoiaMqTFnBykBKeicNxpiav8gTYkvqzEGJ1KS8lSJj8Yl7a2VTubdL8HOOSsbuiaV0IxW3mA8lkg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这样看起来是不是就像带趋势图的卡片图效果，而完全看不到矩阵的痕迹了。

还可以将迷你图改成柱形，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOjIEcl2EAiaCeM5ib0YXoINa5OCxiclRCD0rQwriaSItvkVHTuBTllpSRWZ0ia4d46YkeQddqwvRiacl5w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

使用矩阵制作这种效果，还可以根据需要添加更多维度的数据，如果有每个产品的在线图片，也可以直接放到矩阵里显示出来，比如这样来显示：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2NIfoiaMqTFnBykBKeicNxpdt8BgM02bC5HL4cTGoLc6Nr5319ShSeE1SB08lnqvgSukUfx0yQ0Vw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这样来显示指标是不是更具个性呢！

这里主要就是灵活运用矩阵新的迷你图功能，并熟练掌握矩阵的各项细节设置，建议动手做一遍，矩阵的细节设置如果还不是太清楚，可以参考：

[Power BI矩阵格式设置13招](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071983&idx=1&sn=3fd379f7bf88141747ac9a09dc4273b7&chksm=8e0c44f8b97bcdee4cb068fd1e47e033629cf0734dd29c8341746d449372068dbb4e6d298cba&scene=21#wechat_redirect)  

[**PowerBI星球的最新版****内容合辑****，值得你收藏学习：**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN8YOicNXzCaSLpQrKXOL0LsNeYw0fj3iaGFy7XSwwmibHicdtiaHEbhgmHSPXQlkg3WiaVA4hJ8PGDcdEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078675&idx=1&sn=07abf841815e43fb0a554081c82de72a&chksm=8e13a284b9642b92d07b518abe3e6e2e2ef5066c0941c1ced26a245a6990b4330830431789a9&scene=21#wechat_redirect)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
