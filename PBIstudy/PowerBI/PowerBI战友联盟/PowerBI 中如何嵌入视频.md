---
create_date: 2022-06-06T13:10:19 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 中如何嵌入视频
source: https://mp.weixin.qq.com/s/hK78ah26KWVZc2cyy_tEpA
author: 
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月06日 20:00 直播

PowerBI

视频号

很多小伙伴问如何在 PowerBI 中嵌入视频。

方法非常简单。

## 思路

PowerBI 的界面是 HTML 页面，所以只要可以嵌入符合 PowerBI 允许的 HTML 内容即可。

恰好，使用视频是允许的。

## 控件

首先需要使用第三方控件：

## 度量值

编写度量值如下：

```
HTML.Video = "<video width='320' height='240' controls='controls' autoplay='autoplay'>  <source src='https://files.excel120.com/movie.mp4' type='video/mp4' /></video>"
```

该度量值是 "" 括住的一段文本，由于使用了" " 号，那内部的 HTML 都只能使用单引号。

其中的：https://files.excel120.com/movie.mp4 就是一个在网上的视频内容。

用户可以替换成自己的视频网址即可。

## 效果

使用效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LMnWVR4DAES7uicY20feL7WtjsXvJdkC1ibdNg8OjSe6HJt7EMIalF5C7SsyXRaGWrmTvzhfVQ28Kwg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

## 扩展

将视频的网址保存在一个列表中，然后通过度量值动态赋予控件视频网址，还可以实现动态播放。

大家自己试试吧。

更多精彩，尽在 PowerBI 直播。

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月06日 20:00 直播

PowerBI

视频号

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
