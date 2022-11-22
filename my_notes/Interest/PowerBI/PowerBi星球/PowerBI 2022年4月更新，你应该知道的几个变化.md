---
ZK: Origin
notes: False
aliases: null
create_date: 2022-04-17T11:54:26 (UTC +08:00)
tags: wx/pbi/数据处理功能
pagetitle: PowerBI 2022年4月更新，你应该知道的几个变化
source: https://mp.weixin.qq.com/s/GReBL_mlC9BRLcOLFjQJQg
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

Power BI 2022年4月的更新来了，本月没有什么突出的亮点，主要是对前期功能的优化，你可以在官方博客中浏览全部的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-april-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

这里我主要挑选几个可能会对你有用的新功能简要介绍一下。

#### **1\. 新的格式窗格优化**

新格式窗格自 11 月以来一直处于预览状态，并在 2 月的版本中默认为用户启用。作为提醒，新格式窗格计划在 5 月使其普遍可用 (GA)，这意味着下个月用户将无法再切换回旧格式窗格。

本月添加的改进包括但不限于：

-   形状图自定义颜色已重新添加
    
-   散点图“显示空白值”切换已重新添加
    
-   重新添加了具有滑块类型（之间、之前、之后）响应切换的切片器
    
-   按钮图标大小设置已重新添加
    
-   修复了导致文本输入框光标位置延迟的错误
    

#### **2. 工具提示支持矩阵图、折线图和面积图的钻取操作**

去年发布了现代可视化工具提示功能的预览版，该功能允许从工具提示本身向下钻取数据点或钻取操作。初始预览不包括对一些内置视觉效果的钻取支持；然而，在本月已将此功能添加到更多视觉效果中：

-   矩阵
    
-   折线图
    
-   面积图
    
-   堆积面积图
    

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMSTOH7IyGoHVdezA5pdYyDIAQUStRe2qRWXRehoLFhlstt6LrqRKRH5viaiaweicrqHdRUXxw7Vic1ug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### **3\. 簇状****柱形图和条形图支持误差线**

上个月折线图引入了误差线预览功能，以帮助您可视化数据中的不确定性，具体用法可以参考：

[PowerBI 2022年3月更新，折线图支持添加误差线了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079538&idx=1&sn=db3d9ce423d4c771891cd86e586fb9c6&chksm=8e13a165b9642873e5162a3b25f7ad2bd1b0e04e0f572cc77fc7195642806869e545cfd74e7e&scene=21#wechat_redirect)

现在，误差线也可用于簇状柱形图和条形图了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMSTOH7IyGoHVdezA5pdYyDB5o5zuKwQqKibHQP7z6BFrXY3nrjrfhDyXPV5VtlmyTKRl7QDLCkYnw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### **4. 书签导航器现在可显示每组最后选择的书签**

关于新书签导航器，现在可以在导航器上单击书签后，无论报表状态如何变化，它都会继续保持选中状态。这种小的行为变化允许使用多个导航器以单独的书签组为目标来操作并拥有独立的“活动”书签。

例如，假设您有两个书签导航器，一个反映您为按国家/地区过滤报表页面而创建的书签组，另一个反映您为按十年过滤而创建的书签组。以前，选择十年会清除国家/地区选择，反之亦然，即使从国家/地区选择中应用的过滤器仍处于活动状态：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMrCniaicR5CeERwYpbwXlApqCCTNnoqXf2HnB1gYhlNYZtjS43mWo5Vz3JqVg1WauBiaCpCeWFkVacQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

但是，现在两个书签（选定的国家和选定的十年）将保持选定状态：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMrCniaicR5CeERwYpbwXlApqXZgDtx2qGDRa5oOFibvBjGQUFDhFGfWnv1II3B6Jps4dIqsQ1niciapKQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

请注意，您仍然可以在不选择另一个书签的情况下更改报告状态以离开该书签捕获的状态（例如，通过手动将过滤器从欧洲趋势更改为美国趋势）。与现在一样，您的书签导航器仍将保持其选择状态。

#### **5. **动态 M 查询参数功能GA****

动态 M 查询参数功能现已普遍可用 (GA)，不再是预览功能！此功能允许报表查看器使用过滤器或切片器动态设置M 查询参数的值。这对于那些需要查询性能优化而又不牺牲报告交互性的人特别有用。

作为此 GA 版本的一部分，动态 M 查询参数现在与以下 AI 功能兼容：

-   问答
    
-   分解树
    
-   关键影响者
    
-   异常检测
    

关于动态M查询的介绍和具体用法可参考：

https://docs.microsoft.com/zh-cn/power-bi/connect-data/desktop-dynamic-m-query-parameters

#### **6.** **移动格式化选项支持视觉交互**

在此版本中，将视觉交互支持扩展到了新的移动格式。现在，当您使用新的移动格式选项创建移动优化报告时，您的视觉交互设置将应用于移动布局以及在您的手机上查看报告时。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMSTOH7IyGoHVdezA5pdYyDicmyWiag6bdQpLia85ibYHOwictJaPQ25xIBXiaR4TgiaJFo8wyz3ugsgib41A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

本月的更新就简单介绍这几个，更全面的功能可以去看官方博客继续探索，或者视频号中观看中文字幕的视频讲解。

___

PowerBI每月更新后，如果不能自动更新或者不方便下载，可以在公众号后台发送"**软件下载**",获取最新的PowerBI Desktop安装包；

如果要下载历史安装包，也可以发送**6位年月编号**获取，比如发送“202109”获取2021年9月的安装包。

更多安装说明请参考：[关于Power BI的下载和安装，你想知道的都在这里了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078648&idx=1&sn=7e53496bd78498ed962696055a500474&chksm=8e13a2efb9642bf98bb73de730c5141d61eb2dfd22e1781c2603745137302ea56ba2ae4dd6ba&scene=21#wechat_redirect)
