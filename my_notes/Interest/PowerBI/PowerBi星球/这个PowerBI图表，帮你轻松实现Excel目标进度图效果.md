---
create_date: 2021-08-22T22:46:48 (UTC +08:00)
tags: 
aliases: null
pagetitle: 这个PowerBI图表，帮你轻松实现Excel目标进度图效果
source: https://mp.weixin.qq.com/s/_YJ2ZW4VlFnb-JZ-PedahA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

今天周末，分享一个可视化图表。

经常有人问我，怎么在PowerBI中制作下面这种目标进度图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwLNNiaazrUZ0D5Dr2uTCaX9UzL5me9dR5IiabLOfibaoW8DYiavL4xVGja9D7LdQEibjz26JzLPNsXiag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种图表很常见，经常用于目标和实际对比分析，在Excel中可以轻松制作，就是一个普通的柱形图，利用次坐标轴并调整分类间距，将柱子叠加起来就可以了。

但是在PowerBI中，虽然有柱形图，但还不够灵活，没有和Excel类似的设置选项，无法将柱子重叠到一起，只能做成下面的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwLNNiaazrUZ0D5Dr2uTCaXff1rZf6IY96LN3sP5B6toKupSsNeLSbbLyc8pestZzoiabzIR4IHDyg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

虽然PowerBI内置的柱形图无法实现，但PowerBI中还有丰富的自定义图表库资源可以利用，在里面我就发现有个图表，基本可以实现上面的效果，它就是：

## **Bullet Chart by OKViz**。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTknPqLWWrlKXNxTewzOs2RK7N6w7tWhSdLPfWwCicyucv8nwGVq9P70zQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以前我曾介绍过一个子弹图（[PowerBI自定义图表：Bullet Chart子弹图](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067972&idx=1&sn=2c80350cedd7adca10b6ddaa9289912a&chksm=8e0c7453b97bfd455ff87a43ea151d84f87b75daa8e1ab7025f20d1cbdfd04d99f1bdce69960&scene=21#wechat_redirect)），不过它做这个图也不灵活，所以这篇文章就带你认识一下OKViz的这款子弹图吧。

首先在PowerBI Desktop中加载该图表，它很容易理解，制作起来也简单，将字段分别分入到对应的字段框中即可：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkJsrqkGfW6n0QqF186muWcaJzEGcR0MsFfTCoy604dmBYfkuRVq8J6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

格式调整一下就可以实现这个效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwLNNiaazrUZ0D5Dr2uTCaXDpC9iaVhvYnVSN7DhggAd7G4x5tQcXx0xEHiap3C2fPjUQI2H0HRGyhA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是与Excel制作的效果比较接近了。  

除了能显示数据标签，它还可以直接显示与目标的差异情况，在"Data labels"中设置显示差异比率：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwLNNiaazrUZ0D5Dr2uTCaXrSgFr6QVk2GmHwFeju6DiaG8QvLibUib90tWRBbETEIV5XZWAOJx75khw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

除了上面横向的效果，还能调整为纵向显示，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwLNNiaazrUZ0D5Dr2uTCaXzQwfvdoiaa7T45yxPsxUTeaAKSXELwKsDUORCHfdLZckibLCrxU9EmfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当然作为子弹图，它不仅可以制作上面的简单图表，还可以设置更多的目标值，将多个目标字段放置到Targets中，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkL4SBmSWLV1tZblOLiaQVLKWmzDDS6QyLXDCxL9QhWnEkFdiaqTEuMn8A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就可以直观展示相对于多个目标的完成情况：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMwLNNiaazrUZ0D5Dr2uTCaXAFF9Lq3aXoWEibgspS7kuRmjkSeRtcV7H6Ee7CX7dSnku7y31l2kicDQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个图表用起来没有什么难度，但效果还是不错的，在自定义图表中也算是很好用的一个，并且完全免费，当你需要目标和实际的对比分析可视化时，也可以加载这个图表试试。  

本文示例文件可以在「PowerBI星球」公众号对话框中发送“**Bullet Chart**”获取。

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkvUibMVjf4z1bY0MYFh7lAkqrcHiaEHE4UicvjJjibpmkxJjc4TDlVO04qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOojexubCy39PJZJic24XlI9IC8Fhx57SVYiciave3T7sAxeLXXZgrAzhAsUHXC3dxpU1fp72ChD8ibfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
