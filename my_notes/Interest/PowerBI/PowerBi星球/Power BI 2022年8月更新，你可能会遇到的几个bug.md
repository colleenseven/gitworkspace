---
ZK: Origin
notes: False
aliases: null
create_date: 2022-08-12T12:23:40 (UTC +08:00)
tags: wx/pbi/数据处理功能
pagetitle: Power BI 2022年8月更新，你可能会遇到的几个bug
source: https://mp.weixin.qq.com/s/iWLBmG92RKkkoTM2ByRfkQ
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

Power BI 2022年8月已更新，你可以在官方博客中浏览全面的介绍，点击最下方的阅读原文也可直接进入：

https://powerbi.microsoft.com/zh-cn/blog/power-bi-august-2022-feature-summary/

还可以在视频号中观看本月更新的微软官方视频讲解（已加中文字幕）:

本月的更新没有让人心动的功能，我不再介绍了，而明显的bug倒是有几个，这里根据这两天大家的反馈整理如下：

#### **1\. 打开文件报错**

有人升级后打开一个之前正常的文件，在报告上方会出现错误提示，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0pGrCgk1R0hguRxJ19szphXCzJd71gmjEfmhT2khmjo3usz83oaoe7IYLia19H6FhCgHPptaWIlg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击"应用更改"无效，点击"放弃更改"会遇到类似这样的弹窗报错：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJP0pGrCgk1R0hguRxJ19szpRLFxgSdgGUDxeumD5wPaxNhiaFJYVWBpxxe87sS4IIwI0EtaHwtqEqQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于这个报错，猜测与PowerQuery中创建的参数有关，可以进入PowerQuery编辑器中，点击所有的参数后，再重新上载到模型中，这个报错会消失。

当然更简单的方法就是不要更新，退回到之前的版本，一切会恢复正常，应该是由于8月版本bug导致的问题。

#### **2\. Shift + Enter无法缩进**

8月更新专门列出的一个功能更新是DAX编辑器改进，不过尝试过之后，没有体验到改进的地方，倒是有个明显的错误，在DAX编辑器中，**使用Shift + Enter只能换行，不能缩进了**。

关于DAX编辑器常用的快捷键，可以参考：

[分享21个相见恨晚的DAX编辑器快捷键](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077119&idx=1&sn=9460a984173d3fd46896c2c263b89a1b&chksm=8e13a8e8b96421feb964c24c53a4fcc8198da9d83426cc46905af459ad927723821527af1ddd&scene=21#wechat_redirect)  

#### **3、Ctrl+Z撤销操作时，会删除视觉对象**

当你从AppSource中加载了一个自定义视觉对象，用它作图以后，如果不想用了，当你使用快捷键“Ctrl+Z”撤销操作时，会发现不仅仅把步骤撤销了，竟然把加载的视觉对象也从报告中删除了，不得不再次去AppSource中加载。
