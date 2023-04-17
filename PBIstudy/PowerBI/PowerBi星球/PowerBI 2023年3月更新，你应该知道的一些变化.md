---
create_date: 2023-03-19T23:28:10 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases: null
pagetitle: PowerBI 2023年3月更新，你应该知道的一些变化
source: https://mp.weixin.qq.com/s/mx3uE-p1Mz9hb9AN0_oZUw
author: 采悟
status: 已完成
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

PowerBI 3月的更新如期而至，这次更新对可视化界面和操作方式带来巨大改变，对初学者更加友好了。

关于本月的更新你可以在官方博客中浏览全面的介绍，点击最下方的阅读原文也可直接进入：  

https://powerbi.microsoft.com/zh-cn/blog/power-bi-march-2023-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

这里我挑选几个你应该用到的更新带你浏览一下。

**1\. 新的可视化操作界面**

本月PowerBI Desktop启用了新的可视化界面，前几天已经专门介绍过，请参考：  

[Power BI界面重大改变：感受Excel般的熟悉与便利！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484084036&idx=1&sn=f71658deb7e0f453a5e69532c532b30a&chksm=8e13b793b9643e85353092860cb8e24fedce33a15449c219f9bae19bbb0b6c5147c33e524bbe&scene=21#wechat_redirect)  

除了界面的调整，还大量加入了右键操作，对于初学者、习惯使用Excel的人来说，使用体验会更好。

如果你不是很习惯这种样式，现在也可以在预览功能中去掉“对象上交互”的勾选，继续使用原来的界面。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPG31fYGjiaxRoPh1r4ogNq5bEn5UfOzWInSBoPnDD4ofP1IMe320UicVYU6npOdXJicmw0uGMUWw03A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

不过建议还是勾选上，慢慢适应新的界面，因为过几个月普遍可用后，就会强制使用新的界面了。

**2\. 图表标题格式更丰富**

图表的标题可以直接双击编辑。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPh19icx0jJ0Q7luE6nfiaMibggbwaxSE1OOxcKRUbJcjNoHFzU5pMAasicdqtjic98WHn5Jeyu5QEdvxQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

并且现在可以对标题进行更多设置，打开标题的格式面板，你会看到三个新的选项：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPh19icx0jJ0Q7luE6nfiaMibgw5SRb2FGJA2QiauTLTmjq2HyCt5PEibkibAFfKktUvpz1HFNLmJzicMjBg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

仅仅看这些名称可能不知道是做什么用的，其实他们的作用是：

-   **字幕：**副标题
    
-   **分割线：**标题和图表之间插入一条分割线
    
-   **间距：**设置主副标题之间、副标题与分隔线之间、以及分隔线与图表之间的距离。
    

设置了字幕(副标题)和分隔线的效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPh19icx0jJ0Q7luE6nfiaMibgJNyOy1BmZOTicSrfdP9quZ4zZkjKkS96tt70PYkeWnkpdiaTUhdgY6Ng/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

有这几个选项后，标题的设置更加灵活了。

**3\. 图表四周边距可自由调整**

现在还可以对图表四周与边框的间距进行调整，选中图表，展开 大小和样式>填充：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPh19icx0jJ0Q7luE6nfiaMibg83xnSFBL9RXH2s5vBlJBdoQozIJfZnTcicyGAyte9AhE8rI3Zlicm1dQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后就可以通过调整上下左右的数字来改变图表与边框的每个间距。

4**. 新增切片器全部应用/清除按钮**

如果页面上切片器较多，报告数据还比较大，那么切片器每选一次，其他图表都要开始转圈圈刷新等待几秒，是非常糟糕的体验，如果选好所有的切片器以后，再一起刷新就好了。本月新增的“==应用所有切片器==”按钮就是解决这个场景的。

除了“应用所有切片器”按钮，还新增了“==清除所有切片器==”按钮，点击可以直接清除所有的切片器选项，恢复到无筛选的状态。

这两个按钮可以通过下面三种方式来添加。

**4.1 从优化功能区插入**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMa29P4y37kuy9X8ica0jdhX3H8LazsHdveOKvqHaibLcUngjhlEW1U9QnnHYIIfNian3dJBrwxATWcg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

功能区上只有“应用所有切片器”按钮，其实添加以后，更改按钮的文本和操作属性就可以变成“清除所有切片器”按钮。  

**4.2 插入>按钮:“应用所有切片器”**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMa29P4y37kuy9X8ica0jdhXWldD7NvTNzhyaWGFLxQ6TVWdhgpLI1sB2xVFz7cQwxkN53EzJ5hJqA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**4.3 插入任意按钮，调整操作属性**

选中任意按钮，可以在操作属性中调整成为“应用所有切片器”按钮、“清除所有切片器”按钮。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMa29P4y37kuy9X8ica0jdhXMsPqA95lNFgIfpkiaragw1L1AibkB0xch4wQicQqMHDibfGakSotXapXnQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**5\. 支持单个图表嵌入到PPT**

现在支持嵌入单个图表到PPT，并在PPT中生成数据见解，详细操作方法见：[PPT支持PowerBI单个图表插入，并自动生成数据见解](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083940&idx=1&sn=62aa5bd8122083aebd437ac96c022ee4&chksm=8e13b633b9643f25b15c921a54fae42c9670961c88388ce5b2ce3cb04b2db9bae41ac630fd9d&scene=21#wechat_redirect)

本月的更新就简单介绍这几个，更全面的功能可以去看官方博客继续探索，或者视频号中观看中文字幕的官方视频讲解。

本月更新内容中还提到2024 年 1 月 31 日将停止对 Windows 8.1 上的 Power BI Desktop 的支持。之后，Power BI Desktop 将仅在Windows 10 及更新版本。2024 年 1 月发布的适用于报表服务器的 Power BI Desktop 将是支持 Windows 8.1 的最后一个版本。使用win8系统的伙伴可以关注一下，建议早点升级装备。
