---
create_date: 2021-08-16T22:50:50 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 2021年8月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/EIMPlJnxXKnI8unyENrkjA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

PowerBI 2021年8月的更新来了，关于更新的完整内容官方博客的介绍非常详尽，你可以在博客中浏览（使用Chrome浏览器可自动翻译）：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-august-2021-feature-summary/

也可以在我的视频号中观看本月更新的官方视频讲解（已加中文字幕）:

这里我主要挑选几个你很可能会用到的功能简要介绍一下。

**1\. X轴恒线改进**

## X轴恒线值现在支持自定义了，这个功能虽小，但非常实用，选中图表，打开分析面板，就可以看到它：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNkXwl3d20PU9cID8VPeZnx5M279fSwO6wfOib2AmHLowqy3r92Jmrjo5f8zjxE2fC4MQ2EGJoaibPQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**在值的旁边，有个fx按钮，点击进去，就可以将度量值放进去，这样在X轴添加动态的辅助线就非常方便了。**  

比如之前我做过的[盈亏平衡](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074680&idx=1&sn=a3607ef748c8fbdae96dbec508eb4444&chksm=8e0c526fb97bdb79703e4ac355c51cf3f5983ef09a093043ad21610550fe57f5aeb67de9a38b&scene=21#wechat_redirect)分析（[如何用 PowerBI 做盈亏平衡分析？原来这么简单！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074680&idx=1&sn=a3607ef748c8fbdae96dbec508eb4444&chksm=8e0c526fb97bdb79703e4ac355c51cf3f5983ef09a093043ad21610550fe57f5aeb67de9a38b&scene=21#wechat_redirect)），为了在x轴添加辅助线，用的是折线和柱形组合图，并动用了很多技巧才达到效果，但现在利用这个新功能，制作起来就超级简单：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPAkD9ib9iaV6nBEb29PicmWvyibYwEvuyuiaibUZib3IDic83Qg29R7SgKk3PhdRD3Ablz0Gteiaicz3bNPvYA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

并且还支持在辅助线左/右添加阴影：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNkXwl3d20PU9cID8VPeZnxJcHBM3KEuxfjibsoCJ4zibA5YXHcRxS4ewibiaI6mMww8mErxOs7ECI6BA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. DAX中增加表示日期和时间值的新方法**

之前在DAX公式中表示某个具体的时间必须用DATE和TIME函数，比如：  

> //2021年8月16日  
> 
> DATE(2021,8,16)   
> 
> //2021年8月16日11点30分56秒  
> 
> DATE(2021,8,16) +TIME(11,30,56)  

现在表示这些日期时间，可以不用DATE和TIME函数了，新增了一个符号dt，上述的日期和时间就可以直接这样写：

> **dt**"2021-8-16"
> 
> **dt**"2021-8-16 11:30:56" 或者 
> 
> **dt**"2021-8-16T11:30:56"

看起来是不是简洁很多，也更符合我们平时的书写习惯。

**3\. 评估配置设置**

从本月开始，Power BI Desktop 选项中添加了两个配置：

-   同时评估的最大数量
    
-   每次同时评估使用的最大内存
    

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNkXwl3d20PU9cID8VPeZnxIsGXl9yicVOtOVhia5UReorXHqkgfCwBo9jh6rHogjwZEkACJAfGrphg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个功能都还没有来得及汉化

在导入数据或执行 DirectQuery 查询时，如果执行的速度非常缓慢，可以试着调整这两个选项。

三个常见场景的调整指南：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPAkD9ib9iaV6nBEb29PicmWvyDK20Uvc9Bxv8u7LY94cytWv5p6IeJ0y1JpicFfS5Eonb7VQ3N9pFNjg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**4\. 可视化方面**

Power BI Desktop中的视觉商店全新改版，现在进入AppSource就会看到这样的界面：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNkXwl3d20PU9cID8VPeZnxY4kJHFibDbcveZWUF9CUmWvpGE8Lg4I26TjXhicknZVNjtnUjficynFuw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来高大上多了，虽然里面的内容并没有实质变化:)

下面看几个本月更新的图表：

## **Floor Plan Visual by Simpson Associates**

平面图视觉让您可以在对读者有意义的背景下查看数据。可以在自定义平面图之上映射您喜欢的任何指标，提供对现实世界位置的即时分析。

它不仅可以用作数据可视化工具，而且还可以使用它来导航到报告的其余部分。轻松地使用该视觉效果在数据中的多个楼层/级别之间交替，并为报告使用者提供一个灵活、易于使用的导航工具，用于对您的报告进行切片和切块。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNkXwl3d20PU9cID8VPeZnxavIrYiaU47PVCviblKTqsDA76IaHBLHoVhaNwvW0YmjrLicm1DRZj8owQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

## **Timeline Box / Timeline Basic**

## 新增的两个时间线可视化。

时间线轴将年/季度显示为刻度。关键事件数据呈现为带有基于日期标记时间线的文本框或者气泡。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNkXwl3d20PU9cID8VPeZnxoIEjfgZ6wzVic5u1AflvD21ibUfocMhRn50zldc4icHIIw5YumS9yXwxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNkXwl3d20PU9cID8VPeZnxBXowJHnBWrNS8nDXoMQLDxOXoiagkVcPUPZqd2piarEicmFUJ96DqlosQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## **Balance Sheet Visual**

## 此视觉效果以一种每个人都可以理解的方式显示资产负债表。

它按照资产和负债、所有者权益的结构生成类似堆积柱形图的样式，并且可以进行向上/向下显示更明细级别（如流动资产、固定资产），可以更清晰直观的看出资产负债的构成比例。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNkXwl3d20PU9cID8VPeZnxzFJUiaKPMGLicoQClpWU8JnVOibVsGD5JO1hNkKp7vqlJIBTFIia6kpn3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上图表你可以根据需要去探索应用。

关于8月的更新就简单介绍这些，更全面的可以去看官方博客，本月的官方介绍视频中，还详细讲解了轻松增强性能的自动聚合功能，感兴趣的可以观看视频了解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202102”获取2021年2月的安装包（2021年2月是支持win7的最后一个安装包）。

___

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)****[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)****

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPAkD9ib9iaV6nBEb29PicmWvyXnmLrt9jtBVgRU9CiahLiblaa5YnEN3DlTIXA31Iv1PhsTGcHvmzdGdw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
