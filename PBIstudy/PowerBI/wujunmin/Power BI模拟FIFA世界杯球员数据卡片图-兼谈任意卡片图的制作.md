---
create_date: 2022-12-17T00:10:09 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI模拟FIFA世界杯球员数据卡片图-兼谈任意卡片图的制作
source: https://mp.weixin.qq.com/s/PcJlLAy_8XqZTkXu5VLr3Q
author: wujunmin
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

前期有关世界杯的文章：

[_Power BI足球风格条形图_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491136&idx=1&sn=cd0c9a60c8009f660315298339ba8ef1&chksm=97db2710a0acae06e20fe5cd26ba6e8ccb89c5955ce3ba2fbf922d842c2c0229711d676c8cda&scene=21#wechat_redirect)  

[_这份超详细的足球数据值得拥有_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491208&idx=1&sn=985b4c304ebedcee00f265b54483f9ee&chksm=97db27d8a0acaece6f9c32d3eb93ebc91d425ac5d259b62f24d2da03c8f3095e225550ceecf3&scene=21#wechat_redirect)

[_世界杯可视化作品：阿根廷对克罗地亚_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491303&idx=1&sn=18daa2aa7730ec79825f8cec1ed6832a&chksm=97db27b7a0acaea1168313a7e3dea733b038a2f256ec4c6b6bdaca4dbeeae2425d4bed5bb1a4&scene=21#wechat_redirect)

[_Power BI制作世界杯射手榜表格_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491316&idx=1&sn=ee735b12cbd021a9545259516b8dca75&chksm=97db27a4a0acaeb22e9778841995465abb08ec806dd1b2d5b3cd4330b7e205b6d0e52f7e1e0b&scene=21#wechat_redirect)  

FIFA官网有世界杯每场比赛的球员卡片图展示效果，如下图所示。这个布局其实可以在Power BI使用内置表格轻松实现。核心原理是使用SVG矢量图中的文本标签（**参考视频教程**：_https://t.zsxq.com/09AblJCfG_）

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QMDSDOONsxlYeYJAL9R1bqhzIaP4Buv7xbz8jGtKKFcflamKFm3LBOBUHiclLdqdfJwQicBcqabbyg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_来源：https://www.fifa.com/fifaplus/en/match-centre/match/17/255711/285075/400128143?date=2022-12-14_

在模拟之前首先需要研究该卡片图的结构。整体卡片图分为两个部分，左侧为文本信息，右侧为头像。文本信息又可以分为两部分：上方的姓名和下方的数据。

姓名的细节在于，名字号相对较小，姓字号相对较大，且进行了加粗；数据的细节在于数据大小颜色为红色，且进行了加粗。以下是Power BI表格的模拟效果（数据为虚拟）：  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

卡片图的度量值如下：  

```
卡片图 = 
```

把该卡片图度量值标记为图像URL，和头像列放入表格即完成设置。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QMDSDOONsxlYeYJAL9R1bqicF6ic0ozOkPtqSXv98uquibnmNt07Qu49xR6bWm905Lltibn59OUlgfHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到，这个卡片图仅仅使用了text一个标签，通过变化格式和位置达到使用目的，读者在后期自定义卡片图时可直接复用。人物头像可以是网址URL，也可以是[本地图片转换为BASE64](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247490046&idx=1&sn=f399c968180d24318b7abed5a1f206f5&chksm=97db20aea0aca9b86ef50d3504ebc68b5c1ea2b2102868752339963fda2ff7f2d1b1a8d26e42&scene=21#wechat_redirect)。  

这个效果还有点缺憾，人物头像能不能加上所属队伍图标？可以的。这里采用了图像叠加图像的技巧，人物头像列置于表格列，旗帜列置于人物头像列的条件格式图标。  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

条件格式如下设置：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QMDSDOONsxlYeYJAL9R1bqVMujjA8hcE3eGqZ3Tet0EaHicOOBTN80AqFJibEftVeATJhWCPHdPNfg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上文本是左对齐，右对齐也是可以的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TnahyNJRZaRiczutMocqEyJygh1qn4ibo4iavochZEyn39EJT7yiaetVhqzN29dh6icSjRJLRR1iamRGaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

本文配套pbix文件包含下图三种模式，在下方知识星球下载，直达链接（可左下角阅读原文访问）：

_https://t.zsxq.com/09ZRjHfZj_

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TnahyNJRZaRiczutMocqEyJictcHJo0Yb9XFpyrwpTDuTkTjcQzIDUqbAAYJOy1Jsr7sYO5mialCvuQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6SrFOpSISmqT2k74QM76UrbIBKw9vBMzBUmBfibKCas2iccpABJdicQ4UNYGL2QCMLGaesXVyJ601kvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

[详情](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491267&idx=1&sn=9f8011a4c2a7f38f17b6ef4168625c63&chksm=97db2793a0acae853c07277e58d55c0b8db67e953b44228508b7282f4e907af330cf64efbf51&scene=21#wechat_redirect)
