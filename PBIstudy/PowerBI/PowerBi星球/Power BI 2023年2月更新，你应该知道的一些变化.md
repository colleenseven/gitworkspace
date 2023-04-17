---
create_date: 2023-02-17T23:31:47 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases: null
pagetitle: Power BI 2023年2月更新，你应该知道的一些变化
source: https://mp.weixin.qq.com/s/Yt1Zax3djh8cUr4B-PKNRQ
author: 采悟
status: 已完成
category: 泛读文章 
notes: False
ZK: Origin
uid: 
---

PowerBI2023年首度更新如期而至，这次更新带来很多功能上的优化，可以在官方博客中浏览全面的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-february-2023-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

（欢迎点赞、关注我的视频号）  

这里我挑选几个日常会用到的更新带你浏览一下。

**1.** **条件格式支持文本字段**

之前通过界面功能来设置条件格式时，只支持数值型字段（[Power BI条件格式规则，你知道怎么设置吗？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076484&idx=1&sn=f4f8200273b4662fc5a11a0c667c7a92&chksm=8e0c5513b97bdc05413617d78cfc2ac592b067919727b3729fec033b8b861a72f6e1f74289fd&scene=21#wechat_redirect)），而对于==文本型字段设置条件格式，只能通过DAX的方式来实现==。

本月更新后，条件格式窗口新增了对文本字段的支持。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMucfttFGe2eyBsvAorF9NfUibWIliaxb2ibvBcAlBrco34piaARwGSpHJDoyj1uAlAj5ODpOTOc2DLMg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

可以通过鼠标选择，来==判断当前上下文字段是否包含、开头是/开头不是、等于/不等于某个字符串，来设置不同的颜色。==

**2\. 行级安全性编辑器增强**

对于行级别安全性的角色权限设置，之前只能写DAX来表达，而在本月更新后，也可以直接通过界面操作来设置了。  
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMucfttFGe2eyBsvAorF9NflkSzBcZoicibT077d5SIPJe18vybh6mwvbsyVUfLljxnKNVYWuJrLQ4A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMucfttFGe2eyBsvAorF9NflkSzBcZoicibT077d5SIPJe18vybh6mwvbsyVUfLljxnKNVYWuJrLQ4A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
关于行级别安全性的用法，请参考：[利用Power BI行级安全性，限制用户访问权限](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076638&idx=1&sn=04e90c833a99f5a0e9b2baa06b5c4a8e&chksm=8e13aa89b964239f010a579a4bfdb74ce2dd483b7d333d4a797ca03c12752ab75c1a0fa4e05e&scene=21#wechat_redirect)

**3\. 自定义页面导航器的可见页面**

页面导航器之前的一个大问题就是无法灵活控制某个页面是否出现在导航器上，现在终于可以灵活设置了。  

如果不想让某个页面出现在导航器中，直接在下面的设置中去掉这个页面的勾选即可。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMucfttFGe2eyBsvAorF9Nfnriaw1RG2iaicpVV2ibZSm2OzhaW5HBJ1XUDTfjT0pseoKXFqNIoo2YzwQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

页面导航器的具体用法请参考：[利用PowerBI的这个功能，原来设计导航如此方便](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080516&idx=1&sn=0290f2762815188f0b96e03f3f25fe7b&chksm=8e13a553b9642c45ecf32e51e95720e7f82a4ec9691bc00b6aaee95f12fd30e312557f5ce381&scene=21#wechat_redirect)

**4\. 图表标头新增智能叙述图标**

智能叙述功能现在可以添加到图表右上角的标头上了，在常规>标头图表中，打开“智能叙述”即可显示，然后鼠标点击这个图标，就可以自动显示该图表的摘要情况。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMucfttFGe2eyBsvAorF9Nfb9C3bfw2XVjf9icuG2Aic2gSrYRgghs7OrTjOGHJfjVBeeSnnRiaCzmNA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于这个功能之前也介绍过：[利用Power BI智能叙述，生成动态报告摘要](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073801&idx=1&sn=3a6dcd73ed52e77a4159612fe49af3e7&chksm=8e0c5f9eb97bd68889ce7e6ae0af81e62b7ed6b7ea7827deb5ca1ba097c14e4965889736baa4&scene=21#wechat_redirect)

**5\. 表格中支持调整图像宽度**

现在表格(包括矩阵）==支持调整图像的宽度==了，如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMucfttFGe2eyBsvAorF9NfgeX2mDk72YxC1Tu8rCxe9fNUyViaWNkubicNeDXvcEdxvMsn214S7Wog/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**6\. 文本框支持缩进**

==文本框的编辑窗口新添了增加和减少缩进的按钮，可以对特定行进行缩进操作==。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMucfttFGe2eyBsvAorF9NfOe7eiaCz1BCZPp2ccLxfYhibQExe3icdGkAnfDX7f3z1S76MX2uwiaEzNg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**7\. 新增DAX函数：LINEST和LINESTX**

本月新增了两个统计类的DAX函数：LINEST和LINESTX，可以利用==最小二乘法进行线性回归==。

关于这两个函数的具体用法，后面会专门介绍。

本月的更新就简单介绍这几个，更全面的功能可以去查阅官方博客继续探索，也可以在视频号中观看中文字幕的官方视频讲解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202109”获取2021年9月的安装包。

更多安装说明请参考：[关于Power BI的下载和安装，你想知道的都在这里了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078648&idx=1&sn=7e53496bd78498ed962696055a500474&chksm=8e13a2efb9642bf98bb73de730c5141d61eb2dfd22e1781c2603745137302ea56ba2ae4dd6ba&scene=21#wechat_redirect)

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**
