---
ZK: Origin
notes: False
aliases: null
create_date: 2022-10-22T15:27:56 (UTC +08:00)
tags: wx/pbi/数据处理功能
pagetitle: Power BI 2022年10月更新，自然语言生成DAX功能面世
source: https://mp.weixin.qq.com/s/eJNl5pwmEf-RxBw_3JuS9w
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

Power BI 2022年10月更新，增加/优化了几个新的功能，其中最重磅的当属自动生成DAX的快速度量建议，你可以在官方博客中浏览全面的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-october-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

这里我挑选几个你应该会用到的更新简要介绍一下。

#### **1\. 快速度量建议**

几年前Power BI就发布了快速度量值的功能，允许用户使用内置模板创建DAX度量，而不是从头开始编写DAX，之前我也介绍过快速度量的用法：[不知道怎么写度量值，试试这个方法！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067688&idx=1&sn=7c6e715e449557e1a082e22889cc7351&chksm=8e0c77bfb97bfea9f11f37dd7d02ad042a5313b882b4efb833d31a5117a83188310240c7014b&scene=21#wechat_redirect)

不过，系统内置的快速度量值的模板数量有限，灵活性也有待提高。本月PowerBI发布了新的方法，就是**快速度量建议，它可以让用户使用自然语言创建DAX度量，而不是使用模板或从头开始编写DAX**。

现在还是预览功能，所以需要先启用该功能，在PowerBI Desktop中依次打开文件>选项和设置>选项>预览功能，勾选“快速度量建议”，如下图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9wKMTHqHAEPtqTyaAfAyGwiaicia80dbuukNK92yVa5yYRrloXibAGBIEOg2qr1BicwicZtaFW79GqDcg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在功能区点击"快速度量值"，就会弹出快度量值面板，然后点击"建议",就可以看到自然语言的文本输入框。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9wKMTHqHAEPtqTyaAfAyGjqHSLnpTN4kWsGan7txY9vthTkc4kgP18tFpUJHVUA3hjmESBzTKaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想知道排名前三的产品销售额，可以在文本框中输入“_**产品名称 销售额 top3**_”，然后点击“生成”，就会自动生成产品前3合计销售额的DAX表达式，以及预览结果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMO1JF1yIoYMwiaLPxPbzBLEibnpmOH8LOFaMnIQgIVTiamo8KicpiaW4ic2Gz7cia8xZuXvVtLv0m006K1A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是快速度量建议，对于自动生成的DAX，如果验证没有问题，就可以点击右下角的“添加”按钮，然后这个度量值就建好了，与正常的度量值没有什么区别：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMO1JF1yIoYMwiaLPxPbzBLE06FS0A9AE9ETCaia0lW1VQDM1g1XzwJz9lM12VUTXFsrrU48aRd4Ijw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

度量值的名称自动命名为Measure，你可以手动重命名。

**这个功能目前还比较弱，对中文的支持不够友好，业务逻辑识别准确度不高，还不能做到中文自然语言自动创建DAX，所以它还并不能代替你写DAX，对于DAX知识还是要自己学习的。****（毕竟它只是建议，如果你不懂DAX，也就没办法判断建议是否准确）**  

不过现在才是个开始，随着该功能的迭代升级，相信它会越来越好用，能实现的逻辑会越多越丰富、结果也会越来越精准。

后续深入探索后再对该功能做更详细的介绍。  

#### **2\. 堆积柱形图的反向堆叠**

对于堆积柱形图，如果显示图例，并置于图表左侧或者右侧垂直显示，之前的效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9wKMTHqHAEPtqTyaAfAyGRtyMmJcTBPiaJkox9nVsmiaB89E6F38TPafObukvicx8jR3B9mwACc1dA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

图例的顺序与柱形图的顺序是相反的，比如橙色显示的电脑外设，柱形图显示在最底层，而图例中却显示在顶部第一个，给人很奇怪的感觉，本月添加了一个选项：**反向堆叠顺序。**

打开这个开关后，就可以让图例与柱形图的类别顺序一致：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9wKMTHqHAEPtqTyaAfAyGE2xB0MqrK3gtqJOcotGVFmAgUOXdAknr2KOdVlIZwEJQI3Oms06qng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### **3\. 模型视图中新增关系编辑面板**

这也是个预览功能，首先启用该功能：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9wKMTHqHAEPtqTyaAfAyGpyUB4nDpl6puaQhnp60GuCwnTLCyt0KUuX2HsAB8YX1CwAcUiaLEtgw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后在模型视图中，点击某个关系线，就会弹出关系编辑面板：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9wKMTHqHAEPtqTyaAfAyGQAicB0EZey5sbwQ9pQMgMuDS4kko8OR95qYOxibKKrKccfTCuhoMQkSA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过这个面板，可以直接查看、修改所有的关系选项，比如基数、方向、关系是否可用等，更加方便。

#### **4\. 模型视图中支持编写DAX**

之前只能在报表视图或者数据视图中可以编写DAX，现在<mark style="background: #FF5582A6;">在模型视图中，也可以直接创建、查看、编辑度量值、计算列和计算表的DAX</mark>了，这样就不用来回切换视图了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9wKMTHqHAEPtqTyaAfAyGq6fwTdDk9Ogc2TrAhiaDKsOkf2egia15fPA37v966KMaVylicpuQbwfCg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### **5\. 在PowerBI服务中支持下载不含数据的pbix文件**  

从本月开始，在PowerBI服务中下载报告的pbix文件时，您将看到以下对话框：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9wKMTHqHAEPtqTyaAfAyGuuYICY0lgRLAqcPGrIwk9NlHYib2gxrDmOJ8KD331E6mJoozteESV6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如对话框所示，您现在可以选择下载包含数据的报告，也可以选择下载不包含数据但与数据有实时连接的报告。请注意，根据您的具体情况，可能只有一个选项可用。

本月的更新就简单介绍这几个，更全面的功能可以去看官方博客继续探索，或者视频号中观看中文字幕的官方视频讲解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202109”获取2021年9月的安装包。

更多安装说明请参考：[关于Power BI的下载和安装，你想知道的都在这里了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078648&idx=1&sn=7e53496bd78498ed962696055a500474&chksm=8e13a2efb9642bf98bb73de730c5141d61eb2dfd22e1781c2603745137302ea56ba2ae4dd6ba&scene=21#wechat_redirect)
