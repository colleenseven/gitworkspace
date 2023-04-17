---
create_date: 2022-12-02T23:50:39 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases: null
pagetitle: Power BI 2022年11月更新，你应该知道的一些变化
source: https://mp.weixin.qq.com/s/3lkJ2P5tQX-zUPfmOgxsAA
author: 采悟
status: 已完成 
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

PowerBI2022年11月更新，比平时来的迟了一些，月底才发布，不过迟来的更有惊喜，众多新变化一起亮相，关于本月的更新你可以在官方博客中浏览全面的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-november-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

这里我挑选几个你应该用到的更新简要介绍一下。

**1\. 界面颜色调整**

当你安装新的版本，打开就会发现与之前不一样的清爽感觉，欢迎弹窗以及功能区强调色都变成了蓝绿色！
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhc18kYVJM8V7nx1NvVeUu3g1PLpaE3g52l0qbs53VKz01ncByVAiczrjJXQic1wNibqp2AZPOZLNng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhc18kYVJM8V7nx1NvVeUu3g1PLpaE3g52l0qbs53VKz01ncByVAiczrjJXQic1wNibqp2AZPOZLNng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
按微软官方的说法，此更改是为了确保更易于残障用户使用，新颜色提高了对比度并增加了 Power BI 中用户界面的可见性，使体验更易于使用且更具包容性。

Power BI 品牌颜色和图标徽标将继续保持黄色。

**2\. 小多图优化，坐标轴可不统一**

之前==小多图的坐标轴是统一的，如果每个小多图类别的数据范围变化很大时，与最大值较高的图表相比，最大值较低的图表会被推低。很难评估较低图表的销售趋势==，比如下面的小多图，有的产品的趋势图看起来接近水平线。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhc18kYVJM8V7nx1NvVeUuBNd8tib8IU6pialm4xPFTEW6JTAqUlSIEOMGN74PictkeDhk4MWdtktzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有时用户可能不太关心比较显示的数字的绝对值，而只对比较每个类别随时间的趋势感兴趣，所以新版本新增个选项，==允许用户根据单独绘制每个小多图表的Y轴==。

在格式窗格的Y轴中找到新选项“共享的y轴”和“调整大小”，==关闭"共享的 y 轴"并打开“调整大小==”：
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhc18kYVJM8V7nx1NvVeUuSvTa74HHGmArsOfqMEmRedcXRrSscX7Ln7HCMK1GKGLRAfCbMpryeQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhc18kYVJM8V7nx1NvVeUuSvTa74HHGmArsOfqMEmRedcXRrSscX7Ln7HCMK1GKGLRAfCbMpryeQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
然后每个小多图的Y轴刻度将变得不同，折线图也自动缩放了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhc18kYVJM8V7nx1NvVeUu8oDXtcAk6S1H5UTacIq9AAHUNsEmZrCnHFx3lqxVVhLepBeGic1MNhA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样调整以后，每个产品的趋势变化看起来都非常清晰了。

**3\. 字段参数可创建动态切片器**

关于字段参数，之前已经介绍过它的用法，参考：

[Power BI字段参数介绍以及常见应用场景](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080273&idx=1&sn=b985ea8a53854f41a1ba75c0585cb3cd&chksm=8e13a446b9642d5085b1590f38ca7dd36c085269ae2d5d0fe75e09c57fc1ae270158d15d79db&scene=21#wechat_redirect)  

本月更新后，不仅默认启用了字段参数预览功能，并且可以使用字段参数创建动态切片器，以之前介绍的动态坐标轴为例，已经创建了一个参数，效果如下：

  
接下来，只需要复制这个参数切片器，然后选择复制的切片器，右键字段菜单并选择"显示所选字段"：

然后，就有了一个动态的切片器，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPhc18kYVJM8V7nx1NvVeUu39msUmtqSGtHiaJibvszibWywryYryTjyWibeLiaU8qGYFLdCZedTzC4fZQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**4\. 新增优化功能区**

Power BI Desktop中新增优化功能区，可以点击上方“优化”选项卡进入。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhc18kYVJM8V7nx1NvVeUuicmzL1pVZPkciaIibkPwNblnXyIu5icwCcVLia1gFT8SiatiaRGsS477cdVAg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

优化功能区上的创作工具为您提供了以下功能：

-   ==完全控制视觉刷新时间==。切换到优化功能区，可单击暂停视觉效果，当您准备好让视觉对象运行其查询并更新其数据时，可单击刷新视觉对象。
    
-   快速选择并应用根据您的报告需求量身定制的预定义设置组合。单击优化预设上的下拉菜单，在完全交互性、完全查询减少或自定义之间进行选择，以找到报告的完美平衡点。
    
-   方便地==启动性能分析器==来分析您的报表视觉对象生成的查询。
    

本月的更新就简单介绍这几个，更全面的功能可以去看官方博客继续探索，或者视频号中观看中文字幕的官方视频讲解。
