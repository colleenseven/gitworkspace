---
create_date: 2021-06-27T19:50:48 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI 2021年6月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/6TdLVo3Gn-EXkElqa5IpCw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

PowerBI每月的更新可能会迟到，但从来不会缺席，临近月底，6月更新还是出现在了我们面前，关于更新具体内容官方博客的介绍非常详尽，大家可以在博客中浏览（使用Chrome浏览器可自动翻译）：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-june-2021-feature-summary/

也可以在我的视频号中观看本月更新的官方视频讲解（已加中文字幕）:

这里依旧挑选几个大家可能都会用到的功能简单介绍一下。

**1\. 新增分页报告可视化**

期待已久的 Power BI 报表的分页报表视觉效果现已作为公共预览版在 Power BI Desktop 中提供。这个原生 Power BI 视觉对象首次允许您在 Power BI 报告中呈现您上传到服务的任何分页报告。并且因为您可以将 Power BI 数据集中的字段连接起来用作参数值，从而为分页报表提供完全交互的体验，就像任何其他视觉对象一样。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaicVhSJI18NL9ltbxMkAOFOWtu2HSkCypA0j4glza75SOBibuAO4NiaGJvpyn6ovP7L0kv5DGGkoMA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于它的用法，之后会有详细的介绍。

**2\. 面积图透明度可调整**

现在可以设置面积和堆积面积图中彩色区域的透明度。之前，此透明度默认为 60%，本月更新后，在格式窗格的数据颜色卡中就可以调整此透明度。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMiaicVhSJI18NL9ltbxMkAOFePthYxBWI01Up0ZnbCbC07KIfrtLibOhWe0BuSNszzKjWtibqjAKI7Yg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

面积图透明度调整为100%以后，实际上就变成了折线图。  

**3\. 柱形图/条形图支持内部填充**

坐标轴为连续型的柱形图/条形图支持调整柱的厚度，以此来确定柱之间空白的多少，更好的控制图表的外观。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMiaicVhSJI18NL9ltbxMkAOF4JwPFJn5FpSnEECseETL5dOSXrJpNKKSr8YJ09ZhtBgib1IRDib3jMag/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

内部填充设置为0时，更方便作为直方图来使用。

**4\. 小多图支持响应性和条件格式**

本月带来了两个小多图的更新。首先启用了对响应式切换的支持，响应式视觉效果会随着坐标轴标题、坐标轴和图例等图表元素的尺寸缩小而缓慢删除它们，从而为绘图区域提供更多空间。

其次小多图开始支持对多个小图表的标题和背景颜色添加条件格式。单击格式窗格中相应选项旁边的 fx 按钮以启动条件格式设置对话框，然后就可以在其中设置图表元素的着色规则。借助此功能，小标题和背景也可以帮助传达信息。

比如设置多个小图表的背景条件格式的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaicVhSJI18NL9ltbxMkAOFmkjVAExQdGZ0865c4TqdibRzhrRfib4KIOckMBIkeZVqe2Q8Wrp1qDNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**5\. 更新的自定义图表**

**Drill Down Combo Bar PRO by ZoomCharts**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaicVhSJI18NL9ltbxMkAOF4yVzISrr0EWaV3E0AKMDD6sIgNATJ2gZo7ib24KVG8onXbAjZUM4x2Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

允许您以多种方式组合多种图表类型（线、条、区域）、堆栈和集群系列，并为每个系列应用丰富的自定义选项。

## **Dumbbell Bar Chart by Nova Silva**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaicVhSJI18NL9ltbxMkAOFpk1fpBZrZKXh93ptAlh72G5ydCafsPIGPrdFRsg9gFTlfQMUqF1iajw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

该图适合显示两个值以及它们之间的差异。

## **graphomate bubbles**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaicVhSJI18NL9ltbxMkAOFKFENl4DXXoJLmu9JZvDicrPYKoYDRyhzADVkFsqnE4o2ia5ez13W7B2w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

快速轻松地概览数据点之间的分布和关系。可以快速识别模式和异常值，以便更好地进行解释和决策。图形气泡非常适合表示投资组合。它们在圆形图表的帮助下为广泛的分析提供了许多选项。

**Zebra BI Tables 5.0**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaicVhSJI18NL9ltbxMkAOFIRL7mQIB4wcLficUmbGIAiaTamm0lpTSYdC5T7ibBJpj4gNHmYpCzyeyw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Zebra BI Tables visual 5.0的最新主要版本带来了卓越的评论体验、灵活的行格式和许多其他设计选项，让您真正表达自己并确保您的报告尽可能具有可操作性！

## **Zebra BI Charts 5.0**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaicVhSJI18NL9ltbxMkAOFIRL7mQIB4wcLficUmbGIAiaTamm0lpTSYdC5T7ibBJpj4gNHmYpCzyeyw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

最新发布的Zebra BI Charts visual 5.0带来了高级堆叠图表、智能评论等！

以上图表大家可以根据需要去探索应用。

关于6月的更新就简单介绍这么多，本月还有问答功能的改进以及连接器的大量更新等内容，大家可以在官方博客以及视频介绍中详细了解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202102”获取2021年2月的安装包。

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
