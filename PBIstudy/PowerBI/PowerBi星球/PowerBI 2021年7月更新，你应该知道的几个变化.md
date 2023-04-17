---
create_date: 2021-07-24T19:43:31 (UTC +08:00)
tags:
aliases:
pagetitle: PowerBI 2021年7月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/rlwRd69YbJ-iZ2gVaMPCSQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

PowerBI 2021年7月的更新来了，也许是距上个月更新间隔较短，本月更新内容相对平淡，关于更新的完整内容官方博客的介绍非常详尽，大家可以在博客中浏览（使用Chrome浏览器可自动翻译）：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-july-2021-feature-summary/

也可以在我的视频号中观看本月更新的官方视频讲解（已加中文字幕）:

这里我主要挑选可视化方面的变化简单介绍一下。

**1\. 小多图普遍可用**

经过半年多的不断迭代，从本月开始，小多图不再只是预览功能了，可以在PowerBI Desktop中直接使用。

大家经常问小多图在哪里，是不是自定义的图表等问题，其实它是一种作图方式，在正常的柱形图、折线图都可以做成小多图的样式，只需要在字段区【小型序列图】中放入字段就可以了。

比如折线和簇状组合图，在这个图的【小型序列图】中放入产品名称，就会为每个产品生成一个小的组合图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNOTSiakQ6M9tRQ77wMcs7yUSl23Eg4sqYsibAwPaoJib8XBHvNyHwm6NNqqegahhVbribRhoFB9uuSkQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

只要有这个字段框的图表，都支持生成小多图。

另外再说明一下，PowerBI中很多新推出的功能刚开始都先是预览，需要在选项中启用才能使用，过一段成熟以后，就会转为普遍可用功能，当然也就不会再出现在预览功能中，所以大家不要问之前文章中提到的某个功能，为什么在预览功能中找不到了。

## **2\. Power Automate 转为内置**

Power Automate是在今年4月份的更新时上线的，当时还是个自定义图表，需要在Appsouce中加载或者导入才能使用，现在它成了PowerBI中的内置图表，可以像其他内置图表一样直接使用了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNOTSiakQ6M9tRQ77wMcs7yU4F7qrU3rq4Bm326j7uEETd6gsS8ibsS7AI2ouG4Fak9nuPfsvlh1hag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3\. 新增的可视化图表**

## **Multiple Sparklines**

## 可以生成更丰富的迷你图的效果，以获得惊人的视觉洞察力，迷你图支持以下图表类型：

• 折线图/面积图

• 柱状图

• 气泡图

• 圆环图

• 子弹图/条形图

• 正常值（文本、数字、图片网址、网页网址、UNICODES 等）

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNOTSiakQ6M9tRQ77wMcs7yUk42JgCYWicAIPYSnDxPQwEfrgQd2dVFfdPiaCeOZefic00pnT9Nh2ydgQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下载地址：https://appsource.microsoft.com/zh-CN/product/power-bi-visuals/wa200002816?tab=overview

**PureViz Infographic** 

可以让用户使用 PPT 创建自己的视觉对象，并在 Power BI 中轻松实现他们的设计。用户可以使用现有度量设置形状的格式、设置文本字段并为其设计中的任何图层设置动画。  

在 PPT 中完成一个超级简单的设计过程后，您可以将您的设计导出为 .SVG 图像，然后在 Power BI 中选择此文件。然后，您可以利用 PureViz Infographic 的功能来完成您的视觉效果。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNOTSiakQ6M9tRQ77wMcs7yUHXk7YGDoMxFbmCMcaQoVjcfQbkGPNfzZ2iaibARjCibhjV8La7Tpic1Ttw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

下载地址：https://appsource.microsoft.com/zh-CN/product/power-bi-visuals/wa200002756?tab=overview

## **Drill Down Waterfall PRO**

更强大的瀑布图，使用丰富的格式选项来控制图表的外观，交互式缩放和向下钻取将确保数据易于快速浏览。

-   触摸驱动切片器- 使用视觉本身过滤报告页面（不需要外部切片器）。
    
-   图表上的交互——缩放、单击并拖动或向下钻取以探索和过滤数据。
    
-   总计显示- 打开或关闭总计列
    
-   小计- 在数据集中设置显示值或让视觉自动计算它们
    
-   丰富的自定义选项- 分别自定义递增、递减和总计系列（颜色、轮廓、列宽、连接器、值标签等）
    
-   静态和动态阈值– 设置最多 4 个阈值以展示目标或基准
    
-   移动友好- 在触控和多点触控设备上使用
    

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNOTSiakQ6M9tRQ77wMcs7yUwNpXo3EDBWNoWMSqaficeqialibQcY6bbJUXnEM9xmZ9q6iaVqGRsMicshg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

下载地址：https://appsource.microsoft.com/zh-CN/product/power-bi-visuals/wa200000767?tab=overview

## **Control Chart XmR**

该控制图XMR可帮助您确定您的过程控制。当您的测量符合特定标准时，指示器会立即告诉您正在发生的事情。这有助于您确定这种变化的来源。

该控制图XMR由两个图表：上图（X-图）显示数据点随着时间的推移与计算的平均在一起。然后使用计算出的平均值来计算控制上限和下限（UCL 和 LCL）。下方图表显示移动范围 (mR-Chart) 及其平均值和控制上限。可以隐藏 mR 图表。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNOTSiakQ6M9tRQ77wMcs7yUbRGOr1dmJU4ibCKHqicibzJTk2OleFicT09Hy9xG7jktfc3icPZqa7aYVjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下载地址：https://appsource.microsoft.com/zh-cn/product/power-bi-visuals/WA200002515?tab=Overview

以上图表大家可以根据需要去探索应用。  

关于7月的更新就简单介绍这些，除此之外，本月官方博客还大篇幅介绍了敏感度标签和流式数据流，对它们感兴趣的可以在博客以及视频介绍中详细了解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202102”获取2021年2月的安装包。

___

[**新书上市**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtTuz8KBs1WLQiaGY8A0XAV02IfuoqQNQHr0UHvPPOZWSOticN3kyGkR6g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069195&idx=1&sn=2efa6240de0dcd522edef3ac7e5650fb&chksm=8e0c499cb97bc08ae20b16fc5528f9420ca02ade398d95b4d1d952fdb111d8cc65e06029f4b6&scene=21#wechat_redirect)

[![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069915&idx=1&sn=57c8d756ba43f7bb21860eccc908ec1c&chksm=8e0c4cccb97bc5da9b6e3452d50f1e5062ed3574dc429149902f5f413ec6f7c8bdb0a88b326c&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和 3k+ 学习者一起成长
