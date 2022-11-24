---
create_date: 2022-05-17T13:14:42 (UTC +08:00)
tags: 
aliases: null
pagetitle: 99% 用户在 Power BI 云端报表常犯错误
source: https://mp.weixin.qq.com/s/WBYgzlvTEjIzVBIWWf9G8A
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

大部分伙伴都会在 Power BI 桌面端设计报表，由于在设计的时候没有考虑到很多细节，导致做了很多以后再发布到云端的时候，会出现很多细节问题，即使是有经验的选手也都常常难以避免。在云端交付给最终阅读者使用的时候，一旦在这些方面出现问题，从严格的洁癖意义上来说：一旦出现以下问题，Power BI 报表视为零分。从这个意义上来说，几乎没有人做出及格的 Power BI 云端报表。

对于咨询公司而言，以下问题几乎是面试的必考题。

## 隐藏标头图标

通常来讲，标头图标对于阅读者是没有意义的，而不应该提供这种复杂的信息给阅读者，因此，应该隐藏。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM8QDWbb3ah6aMVElYTsFubZhQLtNdP3Rz5iaMrp5iaicGNAfpzicu1X792ia0iaXvS0sVJExric8GYliajibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

所有的可视化对象都有这个设置，有三种方法可以关闭：

-   方法一：手动依次关闭。如果你第一次知道这件事，你的报告已经做了几十页，那你的灾难来了。
    
-   方法二：通过主题设置关闭。
    
-   方法三：通过云端设置关闭。
    

对于方法三，设置最为简单，如下：

设置如下：

即可。

但即使如此，还是推荐在 Power BI Desktop 端手动设置视觉对象标头隐藏。

## 打开维护层顺序

这又是一个非常容易忽略的问题，可以没有后续一次性挽救措施。

先来看看现象，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/09hv4Xua0LM8QDWbb3ah6aMVElYTsFubB71GszwpPRiayAqRibZQYricbVFqQxw14d1T9Dx8xJkzAlX1UEybFuGLw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

当鼠标选择了某个可视化对象后，会将该对象置于顶层，导致其他对象被遮蔽，这在绝大多数情况不希望发生的。

需要在 Power BI Desktop 设计时，进行设置，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM8QDWbb3ah6aMVElYTsFubZlicJmomJAiaGC7Gj4mHbhT51SZmRoFKib2eaje2UGb9BU1Kb90DjIGSA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

准确来讲，这里应该用 “维护”=“维持”=“保持” 层顺序，的语义。意思就是，在用户点击某个可视化对象时候，也会保持原有设计时的层顺序不改变。

## 关闭响应开关

响应式是一种根据屏幕尺寸动态伸缩以适配的技术，但在 Power BI 的云端显得有些鸡肋，固不推荐使用。如下：

注意：某些元素有 “响应式” 开关，而某些是没有的。

## 设计布局系统

如果说以上三项是有明显错误的，而布局系统不会带来任何错误，但良好的习惯是一切的开始。

在 Power BI 的选择窗口是可以对视觉元素进行名称设置的，如下：

有了这样的排布，可以让整个布局更加受控。

这是进阶到 Power BI 可视化高级的必经阶段。

## 总结

如果说本文所属的四点用作 Power BI 报表设计的实践，那么，便可以打造出非常细腻的报表；相反，如果用这四个题目去考一考 Power BI 选手，有多少人能真正知道这些的区别呢。

## 预告

为了让大家可以更加方便地使用 Power BI，我们正在基于默认 UI，优化一套 Power BI 默认元素，以便大家使用，该模板可以直接使用。

预览如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM8QDWbb3ah6aMVElYTsFubMSGEYib5icuf1K5JIWArZPSSrJOmeibIAIVkJBuJPoAYCkrJXVWMsPGYw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM8QDWbb3ah6aMVElYTsFubqRE8N99FQnhryBO8KN2Pu6EA4xiaMR2S8mYgEhItYGIUGoIPt1REbjQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM8QDWbb3ah6aMVElYTsFubZgIUW10ic08oJyKP6kgrRXes4X2qicUZjCspQnCRJvfYsZrLdOCmrZMQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

我们会在后续的文章逐一来解释 Z-UI 的构建细节。它应该满足：

-   提供一套框架，可以复制粘贴式地直接用于可视化设计；
    
-   可以自适应任何主题颜色，而都显得美观；
    
-   可以全自动生成导航系统；
    
-   可以支持多级导航的复杂系统；
    
-   其他。
    

我们称该系统为：“Z-UI”。目前正在调试中，将隶属于：保持 “BI - 进行时” 激活状态的《BI 真经 - 连续剧》或《BI 真经 - 演唱会》伙伴，敬请期待。如果你还没有订购《BI 真经》，那就与这套顶级内容擦肩而过了。

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
