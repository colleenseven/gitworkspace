---
create_date: 2022-09-01T11:39:00 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何在 PowerBI 中设置数值标签的动态颜色
source: https://mp.weixin.qq.com/s/b-SiV9O9Td7X7zbctRlYVQ
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

PowerBI 的数值标签从 2022 年 8 月开始支持动态颜色了。

首先，需要下载最新版的 Power BI Desktop。

## 渐变色方式

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LODKnicszZ0fx4hQSR9iaY857w9q5fleNwxjDyJHuIVKvqzXNxQibjPNJ6JF6sdibHrEuaM3dYiapvMtkA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在【视觉对象】【数据标签】【值】【颜色】下设置即可。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LODKnicszZ0fx4hQSR9iaY8577Jwukzx6vUc1Tbhtib71jOB9Jky9AHkeS4pHc1hpicEKG9EQvnJWSVDg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 动态标记最大值与最小值

还可以用度量值进行设置，例如标记最大值与最小值。度量值如下：

```
View.Color = VAR vSelectedValue = [Demo.AC]// 极值VAR vTable =     CALCULATETABLE(        ADDCOLUMNS(            SUMMARIZE( 'Dim Calendar' , 'Dim Calendar'[MonthNameCN] ) ,            "@Value" , [Demo.AC]        )        ,        ALLSELECTED( )    )VAR vMax = MAXX( vTable , [@Value] )VAR vMin = MINX( vTable , [@Value] )RETURN     IF( vSelectedValue IN { vMax , vMin } , "Red" , "Black" )
```

> 注意
> 
> 这里的 DAX 用到的《BI 真经》视图型计算方法，不再重复。

这样就可以通过度量值，动态标记颜色，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LODKnicszZ0fx4hQSR9iaY857GOgSiaSX1YXuwRiaLbs9NcsGVGltmSSdnlcj8C6m8kUv9h0JXfoftboQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 扩展创意用法

太多标签比较乱，可以仅仅显示需要的标签。创建度量值：

```
View.Color.OnlyMAX_MIN = VAR vSelectedValue = [Demo.AC]// 极值VAR vTable =     CALCULATETABLE(        ADDCOLUMNS(            SUMMARIZE( 'Dim Calendar' , 'Dim Calendar'[MonthNameCN] ) ,            "@Value" , [Demo.AC]        )        ,        ALLSELECTED( )    )VAR vMax = MAXX( vTable , [@Value] )VAR vMin = MINX( vTable , [@Value] )RETURN     IF( vSelectedValue IN { vMax , vMin } , "Red" , "#00000000" )
```

利用技巧："#00000000" 设置透明度，让颜色不再显示。则可以得到效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LODKnicszZ0fx4hQSR9iaY8571YdmVaknXquFf0878Z1OKHqvL13GGH2XicwasclWv8ia9kv2erJMrj5Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 总结

动态标签颜色又可以做很多事情了。快来试试增强自己的报表效果吧。

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
