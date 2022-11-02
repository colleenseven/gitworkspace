---
create_date: 2022-05-17T11:43:12 (UTC +08:00)
tags: 
pagetitle: Power BI 2022年5月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/gAdHoIfa_u4sSeDWZAbvWA
author: 采悟
status: 未阅读
category: 
uid: 
---

Power BI 2022年5月的更新来了，本月推出了全新的字段参数、画布缩放功能，你可以在官方博客中浏览全部的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-may-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

这里我主要挑选几个可能会对你有用的新功能简要介绍一下。

**1、新增"字段参数"功能**

这是本月全新推出的一个功能，它可以将模型中的列字段或者度量值设置为参数，快速进行各种动态的分析和可视化设计。

这里先简单介绍一下该功能的用法，目前还是预览功能，需要先勾选启用：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjj40hCAicmdib6GS59WR0OlgvpKAJAoJohzQNsOplXZnKk4FFj6J8qlvg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后当你建参数的时候，上面就多了一个选项：字段。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjyPxQBZlHOA1snIxW2AUFgOhnAia1lvZuOfgKJGYDBLg7X0QBLAoOrYQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以之前介绍过的[动态坐标轴](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068004&idx=1&sn=750fce682b8e15757b038d30aa5a540f&chksm=8e0c7473b97bfd65f68616c2ced6fe5a139e11ccd70b933f92bde1278ff02abedbbe377a3f71&scene=21#wechat_redirect)为例，没有字段参数的时候，需要构造一个表，并利用度量值来实现，非常麻烦。而利用“字段参数”，只需要点击几下鼠标就可以实现。

点击新建字段参数，在弹出的窗口中，选择产品表中的产品名称列和客户表中的客户城市列：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjXvic8ZeHcY6seicFvxxkEobRiaWRgIydoKiaasFFz74oPDeJrQxPgTsH8A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击创建，就和之前创建数字参数一样，模型中多了一个参数表，并在页面上自动添加一个切片器：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMj9WicgWdNC2qFS2TNGziaRTEBc9LCq1JNa1ibABgAwsg4XG1BxIxtdsbpA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后将这个参数作为X轴、销售额作为Y轴，制作一个柱形图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjdTmBibI298O556tF2N3cmUvNkjtiaHwExYKaplaxm28jKMZjMG75m7Xg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过点击切片器，就可以动态地切换坐标轴的维度了：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjZib5Vusxm1RBVU1Pcxh1uyKPWdtdeBRDMVpkTBL03XfStkBtSPL1Xsw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

是不是非常便捷！

利用字段参数这个功能，很多动态的技巧都可以重新设计，之后也会介绍它的更多应用场景。

**2、新增画布缩放功能**

本月新增画布缩放功能，可以通过右下角的滑块进行放大缩小：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjeNbUNicu67Wy6XA5h2LJhDulec0meicfu3PPFbFJr4GNIaM5sjfoHzCw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

用户可拖动滑块设置缩放级别或单击缩放百分比以启动缩放级别对话框并输入自定义输入；旁边还有个“调整到页面大小”按钮，快速返回默认视图。

对于报告读者来说，可读性尤为重要。对于报告创建者，这个功能也有助于放大画布以进行像素级完美调整。

**3\. 新格式窗格继续优化**

新的格式窗格自去年底推出以后，不断在优化，并且会在下个月变成全部可用，不能再通过设置切换到旧版。  

本月优化的一个主要细节是可以展开所有子级别的设置。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjd70XE1jG3Cfedn9HQGgYJr0ialwopQcOxHSI8hVSiasDnaxYTIjr46Eg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样在设置各种格式时，可以节省点击的次数。  

**4、组合图支持添加误差线**

误差线功能继续迭代，本月开始支持在组合图中添加误差线。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0m1jPFZm0XQR9Wia691ibMjgJYibYrVA0mTzOfV6fRoyRCxKgqf6sK4ic4PMscOFFIpsT0lJTaUBBMg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于误差线的用法可以之前的介绍：[PowerBI 2022年3月更新，折线图支持添加误差线了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079538&idx=1&sn=db3d9ce423d4c771891cd86e586fb9c6&chksm=8e13a165b9642873e5162a3b25f7ad2bd1b0e04e0f572cc77fc7195642806869e545cfd74e7e&scene=21#wechat_redirect)

本月的更新就简单介绍这几个，更全面的功能可以去看官方博客继续探索，或者视频号中观看中文字幕的视频讲解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202109”获取2021年9月的安装包。

更多安装说明请参考：[关于Power BI的下载和安装，你想知道的都在这里了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078648&idx=1&sn=7e53496bd78498ed962696055a500474&chksm=8e13a2efb9642bf98bb73de730c5141d61eb2dfd22e1781c2603745137302ea56ba2ae4dd6ba&scene=21#wechat_redirect)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
