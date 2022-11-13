---
create_date: 2021-12-17T12:49:13 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 2021年12月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/j0-tl7NVIGswgnB1Y8pJnw
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

PowerBI 2021年12月的更新如约而至，首先补上了11月推出的新格式窗格中明显缺失的功能，本月的一大亮点是表格与矩阵中支持设置迷你图，完整内容官方博客的介绍非常详尽，你可以在博客中浏览，点击阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-december-2021-feature-summary/

还可以在视频号中观看本月更新的官方视频讲解（已加中文字幕）:

这里我主要挑选几个可能会对你有用的新功能简要介绍一下。  

**1\. 新格式窗格功能完善**

上个月推出的新格式窗格，虽然让人耳目一新，但是使用后发现有很多功能缺失，所以11月的版本不建议安装，本月的更新首先是补充了这些明显缺失的功能，比如：

-   按钮、形状和图像的"操作"选项
    
-   常规 > 属性的响应切换和数据限制设置
    
-   表/矩阵的全局文本大小
    
-   散点图的背景 > 类别标签
    
-   分析 > 散点图的比率线
    

除了这些，我发现依然还有些功能缺失，如果不着急使用其他新功能，可以再观望一段，待稳定后再更新。

**2\. 表格/矩阵支持迷你图**

迷你图是在表格或矩阵的单元格内显示的小图表，可以轻松快速地比较数据的变化趋势。这个需求一直呼声很高，终于在2021年最后一个月放出来了。

现在当你使用表格/矩阵时就可以尝试使用迷你图，以下面这个矩阵为例，

右键【值】中的字段：添加迷你图。  

然后就会弹出添加迷你图的窗口，选择迷你图的X和Y轴字段：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMaFgawfN4u65jXIMpQljLIfhMPHbT0icDibDaRcgVnibXohQT87NvFtZnE1o3GyyFfiaOCEpbYk0WiaicQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

显示的效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMaFgawfN4u65jXIMpQljLIplS3bRe6WqKsS1GJ6LWn6TrQfZXxe8ibBreicWBkhthEu7ic0z9QZqzlg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

默认是用折线图来显示的，还可以打开格式窗格，设置迷你图折线的颜色、数据点标记等可视化元素，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMaFgawfN4u65jXIMpQljLICXU1wChkHrgQlib2zclXsjl0fqrDZP3ZzyZj217N33w0UamnM0NWMug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

  

比如用黄色的圆点标记最大值：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMaFgawfN4u65jXIMpQljLIDxyicscq4iczcfgKKBYHdwlu6mBq33Viawu4CXNkuTKrSguzib2KaBUaLA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还可以使用迷你的柱形图来显示：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMaFgawfN4u65jXIMpQljLIrUw57zRGuGZ9nFdtMv5M00HL3QhQkvp0kcsL3Uyic6vZ9kFjWbUDNiaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

出于性能原因，当使用迷你图时，矩阵中的最大列数也将限制为 20，每个视觉对象最多五个迷你图，每个迷你图最多显示 52 个点。

**3\. Power BI Premium 混合表预览**

混合表（Hybrid Tables）十分强大，它是对增量刷新的突破性增强，有助于在查询性能和数据新鲜度之间取得完美平衡。

混合表本质上是一个大表，它具有一个或多个导入模式分区以及另一个 DirectQuery 模式分区。如果 DirectQuery 分区与导入模式分区相比足够小，Power BI 和数据源之间的查询/响应往返应该仍然相当快，而在导入模式下访问大量数据已经超快。导入的和 DirectQuery 的数据作为包含业务定义和计算的整体呈现给用户。

Power BI Desktop中混合表的设置方式见下图，发布到高级工作区以后，将在数据刷新期间自动应用刷新策略并将表分区为混合表，目前仅支持 Power BI Premium 和 Premium Per User。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMaFgawfN4u65jXIMpQljLIYicFGJ0ICdDxDRHFEO9DaZbyT8mVaBGZynw11ur5WdIGy8qf0iasItNg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**4\. Power BI Mobile视图优化**

之前在手机上查看报告时，如果没有设计移动布局，移动应用程序会自动将报告调整为横向显示，虽然你并不想这样，但是无法调整为纵向。

本月 Power BI Mobile 更新中，删除了该限制，现在可以选择以您想要的方向查看任何报告页面，即使没有做移动布局。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMaFgawfN4u65jXIMpQljLIYTgGZFgpVkxiamO3OAfBEDMU3qHm0rRmqNDxlh1Lq7vr10o8kqdknSA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

纵向查看报告时，可以使用两个手指捏合，来放大/缩小页面，以便更清楚的查看某个局部数据。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMaFgawfN4u65jXIMpQljLIMNZkVftWnlJHv7lfO866cXNYIn8OylsnA56ykQV9Otgd8wgEia2qrlA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

12月的更新就简单介绍这几个，更全面的可以去看官方博客或者我的视频号中观看中文字幕的视频讲解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202102”获取2021年2月的安装包（2021年2月是支持win7的最后一个安装包）。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
