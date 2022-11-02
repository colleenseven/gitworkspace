---
create_date: 2022-08-10T12:24:22 (UTC +08:00)
tags: 建模技巧
pagetitle: 在PowerBI中创建日期表，你可能会遇到的3个问题
source: https://mp.weixin.qq.com/s/v7ZsIZlHZ0Dy_60r_PNzpg
author: 采悟
status: 已完成
category: 泛读文章
uid: 
---

日常业务分析少不了时间相关分析，PowerBI时间相关分析离不开日期表，之前分享过日期表的制作方法，参考：

[PowerBI日期表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067654&idx=1&sn=905c186a9cbd91159b6615924a2d5068&chksm=8e0c7791b97bfe87623904f7002cd6cb726f711c6e7a289a36c9a4973964d907493aa2397fe7&scene=21#wechat_redirect)

[分享一个更实用的Power BI日期表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076559&idx=1&sn=e00814afa6a2013e3ba3a19cfb575f39&chksm=8e13aad8b96423ce61ca80169b35047204be5c7e4750491f84d7ff327eba9c093c9aa9a829f2&scene=21#wechat_redirect)  

其中最常用的方式，就是复制以上文章中的DAX公式，在PowerBI中直接生成日期表，不过有些伙伴在操作的过程中，可能还是会遇到一些波折，这里就将3个常见的问题及其解决方案介绍如下。  

___

#### **1\. 系统报错：该表达式引用多列，多列不能转换为标量值**

经常有人给我发这个截图，问怎么办？

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJORNmibUoP55kvDIPKWYpyq1TyzIC6UsEO8WTia7OKLQdORJ1zOxw5BFdOanY6jd7CBRUew6icXfxb5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

明明是复制的文章中的公式，没有做任何改动，为什么会出现这个报错呢？  

**这个问题的原因很简单，就是<mark style="background: #FF5582A6;">DAX公式放错地方</mark>了。**

日期表是一张表，所以你要点击的是"**新建表**"，然后将复制的日期表公式粘贴进去，而不是新建度量值。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJORNmibUoP55kvDIPKWYpyq1kPGfxzBHbX3tQaHLrcW9IwibPEwPqFgR2qqQZD2prZn2WSPCliaNgUMw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当你使用表函数来建度量值时，都会弹出这个错误。即使不是建日期表，如果你以后再碰到这种报错提示，基本可以肯定是同样的问题。

___

#### **2\. 系统报错：CALENDARAUTO 函数无法在模型中找到 DateTime 类型的基列。**

即使没有点错，确实是"新建表"，但是如果你的日期表公式中用的是<mark style="background: #FF5582A6;">CALENDARAUTO</mark>，还有可能会弹出下面这种报错：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJORNmibUoP55kvDIPKWYpyq1c8YicUPdSJ3QNL0DSghB7WruzcVXia6UNWHRD1MYMdbwAVpRsVObSO9Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

CALENDARAUTO函数可以自动识别模型中其他表的日期列，并自动生成涵盖模型中所有日期的日期表，但是<mark style="background: #FF5582A6;">如果模型中没有一个日期列，识别不了就无法建日期表</mark>，所以弹出上面的报错。

**使用<mark style="background: #FF5582A6;">CALENDARAUTO函数来生成日期表的前提是，模型中至少有一个日期列，该列的数据类型必须是日期型或者日期/时间型，并且必须是基列，不能是计算列</mark>。**

关于基列，你可以理解为是从PowerQuery中上加载进来的列，而不是通过DAX表达式生成的列。

所以如果你模型中没有日期型的基列，就不要使用CALENDARAUTO函数来建日期表，改用其他方式来建就行了。

___

#### **3\. FORMAT函数不能正常返回中文粒度**

在日期表中可以<mark style="background: #FF5582A6;">利用FORMAT函数来生成中文的月份、星期等粒度</mark>，不过有可能会遇到它不起作用的情况。  

比如FORMAT( \[Date\] , "OOOO"）本来可以返回中文的一月、二月……，但是它却返回的还是"OOOO"。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJORNmibUoP55kvDIPKWYpyq196ib3oxFtHx7zGPIWEz5Bz47qVWvqYCDMhib1Ze49Y98zd9jAs18LyKA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果你遇到这种情况，可以使用FORMAT的<mark style="background: #FF5582A6;">第三个参数将区域指定为中国</mark>，写成：

FORMAT( \[Date\] , "OOOO" , **"zh-cn"** ) 

然后就能正常显示中文月份了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJORNmibUoP55kvDIPKWYpyq1K4hOG4D20Y2aEbEL4DW53WqbtVw4knQPqVGicFbWjhTsh23OT6rPrLg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于FORMAT的更多用法可以参考：

[利用FORMAT函数自定义数据格式](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067980&idx=1&sn=4c314be995c216a5a6e6f7a49886cc2f&chksm=8e0c745bb97bfd4d1092fadd56e335ccb0d27f38cffeca7d234fef18eaae81da052c7c69900e&scene=21#wechat_redirect)  

[FORMAT函数，原来还可以这么用](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080057&idx=1&sn=273812ae60d7966b64362d2e8f5ec474&chksm=8e13a76eb9642e78a0577d4dd83ea866d49ca21ae60691ed732a6a3b71646162dc6e7dc37de9&scene=21#wechat_redirect)  
