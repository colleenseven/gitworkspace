---
aliases: null
create_date: 2022-02-19T12:23:13 (UTC +08:00)
tags: 
pagetitle: PowerBI 2022年2月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/6PWVCMg6jiV9lqLntGreLw
author: 采悟
status: 未阅读
category: 
uid: 
---

Power BI 2022年2月的更新来了，和往年惯例一样，1月跳过没有更新，本次更新就是2022年的第一次更新，本月的一大亮点是移动布局支持单独调整格式，完整内容官方博客的介绍非常详尽，你可以在博客中浏览，点击阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-february-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

别忘了给视频点个赞哦

这里我主要挑选几个可能会对你有用的新功能简要介绍一下。

**1\. 新的移动布局格式面板**

如果你之前用过PowerBI的移动布局，应该能体会到一个痛点，就是移动布局中的图表只能跟随web布局的格式，无法进行单独的修改，这种情况下，想做出个性化的移动端报告非常困难。

本月更新后，支持在移动布局中单独调整图表的元素格式，比如字体大小、图例位置、标题、背景等，提供了充分的灵活性和无限的设计可能性，以美化和优化您的手机查看报告，并且这些调整对web端的原有报告没有影响。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN14yQeO6mrLMKWcFy0ajELs4pTjMARchYIUK1n06S1A7O8JhkC9kTCNSZKepkFffhY2OMsno0DMA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

设计好移动布局后，将报表发布到PowerBI服务，然后在PowerBI app中就可以看到专为移动端设计的报告。  

**2. 动态M查询参数支持SQL Server**

动态M查询参数可以让报表查看者使用筛选器或切片器来设置 M 查询参数的值，这对于查询性能优化特别有用。它并不是个新功能，但之前仅支持有限的几个数据源。

从本月开始，它可以支持更多的数据源了，比如常用的SQL Server也可以使用动态M查询。

关于动态M查询的介绍和具体用法可参考：

https://docs.microsoft.com/zh-cn/power-bi/connect-data/desktop-dynamic-m-query-parameters

**3. Power BI Windows 应用支持深色模式**

Power BI Windows 应用程序现在开始支持黑夜模式了，在设置>选项>外观中可以调整为深色：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN14yQeO6mrLMKWcFy0ajELZLOGERzRppY0OcQZQv2LglSpJfuBib3epjBgSOibnxPFYeuMrIaZVQBA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

深色模式效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN14yQeO6mrLMKWcFy0ajELHWkuTkeP7X6b7W8SQmiaLroRnfNlwiadrcOPV5D7ESClJT1aMlpy2AEA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

当应用程序处于深色模式时，所有屏幕和对话框都以深色主题呈现，降低屏幕亮度，便于查看。但是，Power BI 内容本身（例如报表和仪表板）不会改变。

关于Power BI Windows 应用程序，有个十分好用的功能是自动演示，之前专门介绍过：[Power BI报告如何像PPT一样自动演示？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073747&idx=1&sn=2f481a1119ca46623c25a717dde2059b&chksm=8e0c5fc4b97bd6d20f8a96796c48362e8c69f2865b998a59667467229c4ef7d356db3e92f6a2&scene=21#wechat_redirect)  

**4. Appsource界面，可以直接下载示例文件**

新的Appsource界面中，现在进入某个可视化对象页面，可以直接下载示例文件，特别方便：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN14yQeO6mrLMKWcFy0ajELeYYibmCkQRmdcIBWwvfZzHiaRdL047heTOpJ1NR8xgYxHU9Yt81CrqmA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

每个图表的用法都不尽相同，特别是偏冷门的图表，即使加载后可能也并不知道该怎么使用，那么参考作者制作的示例文件就非常有帮助。

**5\. Power BI Desktop现在需要WebView2**

最近不少人问我，安装Power BI Desktop后为什么打不开，老是弹出这个问题窗口：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN14yQeO6mrLMKWcFy0ajELq0eBzfFAAcFm8kng54ohjHpicxAV11RRMaGtFvdC8NBe9SOwpDV6YEA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

原因就是现在必须在电脑中安装WebView2，才能正常使用新版本的Power BI Desktop。

如果你安装新版本时遇到了上图的报错，请先下载安装WebView2，下载链接如下：  

https://developer.microsoft.com/en-us/microsoft-edge/webview2/consumer/

(也可以在公众号后台发送关键词"**WebView2**",获取安装包)

注：如果您的电脑已升级到 Windows 11，则默认安装 WebView2，无需做任何操作。

本月的更新就简单介绍这几个，更全面的可以去看官方博客或者我的视频号中观看中文字幕的视频讲解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202102”获取2021年2月的安装包（2021年2月是支持win7的最后一个安装包）。

更多安装说明请参考：[关于Power BI的下载和安装，你想知道的都在这里了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078648&idx=1&sn=7e53496bd78498ed962696055a500474&chksm=8e13a2efb9642bf98bb73de730c5141d61eb2dfd22e1781c2603745137302ea56ba2ae4dd6ba&scene=21#wechat_redirect)

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
