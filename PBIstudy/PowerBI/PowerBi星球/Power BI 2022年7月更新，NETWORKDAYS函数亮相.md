---
ZK: Origin
notes: True
aliases: null
create_date: 2022-07-18T12:27:49 (UTC +08:00)
tags: wx/pbi/数据处理功能
pagetitle: Power BI 2022年7月更新，NETWORKDAYS函数亮相
source: https://mp.weixin.qq.com/s/LPGv2mKD3RCDWLzN7uqapg
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

DAX:: MIN, MAX,VALUES, NETWORKDAYS

---

Power BI 2022年7月的更新来了，你可以在官方博客中浏览全面的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-july-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

本月更新整体来看没有什么亮点，这里我挑选两个可能会对你有用的地方简要介绍一下。

#### **1、误差线功能普遍可用**

[误差线](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079538&idx=1&sn=db3d9ce423d4c771891cd86e586fb9c6&chksm=8e13a165b9642873e5162a3b25f7ad2bd1b0e04e0f572cc77fc7195642806869e545cfd74e7e&scene=21#wechat_redirect)自3月份发布以来，每个月都在不断完善，从本月开始，该功能普遍可用，不再是预览功能。

本月还<mark style="background: #FF5582A6;">为误差线增加了数据标签的新选项</mark>，可以直接在图表上显示上限和下限的数值或者相对百分比，可以直接在格式窗格中启用这些选项。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHFcnWa8MDDIKWEStwYC7zeVKdwKP0gryw770ia79TwGjYBIotljWLgoHW8GfqaJHB50n7xicGH1Ig/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

本月还<mark style="background: #FF5582A6;">为误差线添加了新的类型选项</mark>。现在，除了能够根据您设置的上限和下限选项创建误差线之外，您还可以根据百分比、百分位数和标准偏差选项来确定上限和下限。

此外，本月<mark style="background: #FF5582A6;">误差项添加了一个新的“设为对称”选项</mark>，对于上限和下限相同的情况，启用该选项，只需要一个字段就可以创建误差线。

#### **2、新增DAX函数：NETWORKDAYS**

<mark style="background: #FF5582A6;">计算两个日期间隔的工作天数</mark>，在Excel中有个NETWORKDAYS函数，但是之前DAX中却没有对应的函数，需要变通的方式来实现工作日的计算，参考：[如何用Power BI进行工作日相关的计算？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077728&idx=1&sn=5d7739914cb98e96b7abd32d402aba3e&chksm=8e13ae77b96427615638ed7351de474f87095c983d3d5c745b94ed1c0fc35a87e34ea247683d&scene=21#wechat_redirect)

本月开始，DAX中终于也有了NETWORKDAYS函数，用法与Excel函数类似，语法如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHFcnWa8MDDIKWEStwYC7z5iaknp9Wj6aicLoCw2PCSQQLQQe4CFod5t6XBPjMrKpwOK3nOhy9jvLw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下面来通过两个例子看看如何使用这个DAX函数。  

最简单的用法可以直接这样写，只用前两个参数：

> 工作日数 = 
> 
> NETWORKDAYS(
> 
>     MIN('日期表'\[日期\]),
> 
>     MAX('日期表'\[日期\])
> 
> )

它计算的是所选期间的工作日数，第一个参数是开始日期，第二个参数是结束日期。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHFcnWa8MDDIKWEStwYC7zZ4stRanQbx2qAibnUzy6vAdpGZsm2umOnQZJ0qCqJLfKeAuByWiagcuA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面的计算，<mark style="background: #FF5582A6;">只排除了周末，对于哪一天是周末，可以利用第3参数进行控制</mark>，第3参数是1或者省略表示周末是最常见的周六和周日，如果周末是其他日期，请参考上面的语法，用第3参数调整。

但在实际计算中，工作日数不仅要剔除周末，还要剔除节假日，这就要用到NETWORKDAYS的第四参数：节假日的列表。

因为节假日并没有规律，所以最好还是先做一个节假日表，然后将这个表作为NETWORKDAYS的第四参数。  

剔除周末和节假日的写法如下：

> 工作日数 \=
> 
> NETWORKDAYS(
> 
>     MIN('日期表'\[日期\]),
> 
>     MAX('日期表'\[日期\]),
> 
>     1,
> 
>     VALUES('节假日表'\[日期\])
> 
> )

第3参数剔除周末，第4参数剔除节假日。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHFcnWa8MDDIKWEStwYC7zQ1SSRysdFWDkU6310iaODODrMMEwhHVxibg9icT0xkEp0UJDMuDNlkSIQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果仔细观察上图的计算结果，会发现其实并不正确，准确的工作日数应该是7，但是它返回了6。

这是由于2021年10月9日是周六，但是由于国庆调休，实际是工作日，用NETWORKDAYS只会剔除周末，却不会加上实际为工作日的周末。  

**所以<mark style="background: #FF5582A6;">这个新的**NETWORKDAYS**函数并不是很好用，如果你只想剔除周末，可以用它来计算；但是要剔除实际的节假日进行准确的计算，建议还是用之前的方法来实现</mark>：**

[如何用Power BI进行工作日相关的计算？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077728&idx=1&sn=5d7739914cb98e96b7abd32d402aba3e&chksm=8e13ae77b96427615638ed7351de474f87095c983d3d5c745b94ed1c0fc35a87e34ea247683d&scene=21#wechat_redirect)

本月的更新就简单介绍这两个，更全面的功能可以去看官方博客继续探索，或者视频号中观看中文字幕的视频讲解。
