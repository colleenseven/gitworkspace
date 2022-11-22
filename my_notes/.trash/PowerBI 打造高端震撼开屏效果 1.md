---
create_date: 2022-11-22T13:08:54 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 打造高端震撼开屏效果
source: https://mp.weixin.qq.com/s/fElOEENl0VQWVdYN_d00iw
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

在设计和打造国际顶级 PowerBI 报表的时候，一定需要一个震撼的开屏。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LO8sCh9LUO8S2UbicW00HUNQ2vPu7QE31Rw4rwjJz5qHt6ibEMNj7QkPah0S6Poe4zjKTiaxUePJzCkg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

该开屏效果必须具备：

-   全内置于 PowerBI 中。
    
-   平滑流畅播放，彰显品牌格调。
    

参考案例：

劳力士 PowerBI 案例。

## 实现方法

使用 HTML 嵌入视频。参考：[PowerBI 中如何嵌入视频](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650793971&idx=1&sn=f081c5e09c498b312b16536aa16bafae&chksm=f18ce7e2c6fb6ef4df64a87066719b8ec9f23dacb7ff975a0eb27bf1e78ff5e1c1726a75bd19&scene=21#wechat_redirect)

其中技巧：

在利用嵌入视频的技巧是：

```
HTML.Video = "<video width='1280' height='720' autoplay='autoplay' loop='loop'>  <source src='...' type='video/mp4'/></video>"
```

-   宽度和高度要和原视频一样。
    
-   src 的地址是公网的视频地址。
    
-   autoplay 和 loop 如上设置。
    
-   不设置 controls。
    

## 总结

PowerBI 的设计需要进入下一个阶段了。

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月10日 20:00 直播

PowerBI

视频号

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，可以下载本文案例。

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
