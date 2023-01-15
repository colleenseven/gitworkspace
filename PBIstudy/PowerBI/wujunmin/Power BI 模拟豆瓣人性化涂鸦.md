---
create_date: 2023-01-05T00:06:49 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 模拟豆瓣人性化涂鸦
source: https://mp.weixin.qq.com/s/DqNiXSpCMXjOVJfLR3Vogw
author: wujunmin
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

近日豆瓣发布了2022书影音报告，以下是我的豆瓣页面，不规则的圆圈和波浪线使得报告突破了方方正正、规规矩矩的死板套路，显得非常人性化。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6RWU51CdguFsT15rWKicYMwURkC1Wdkp9EpzsH7IvPyXstMWLibza7NAv0ARHt8ibn2TElfnQiaW5I9uw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

Power BI可以模拟类似的效果，圈圈和波浪线任意手绘，可用于表格矩阵，也可单独卡片图。实现原理是SVG矢量图。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

首先，搜索引擎搜索SVG在线编辑器，随便进入一个，使用铅笔工具按需画个不规则的圈或者下划线，画圈尽量沿着画布的四周，为给数据留下中部的空间；画下划线尽量靠下，为避免下划线与数据重合。  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

画好后，点击文件-保存图片，图片被保存为SVG类型。  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

记事本打开图片，可以看到下面的代码，中间的path就是你画的不规则线条，查找替换把文件中的双引号都替换为单引号。  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

打开Power BI，新建如下度量值：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RWU51CdguFsT15rWKicYMwU2LDuibXTibj43TKNDAE40cmAs96O0hAYKicKPEGxxY2HHsHgreTubesSw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

度量值分为三个部分，起始为SVG标准语法，注意里面的width、height值与你在线画图的画布的值保持一致，此处都是100个像素；中间的path是复制的SVG文件中的path部分，下方的text为你需要显示的数据，此处是一个百分比。  

把度量值标记为图像URL，可以放在表格矩阵使用，也可使用ImageByCloudScope视觉对象作为卡片图使用。  

接下来有个问题，颜色可否自定义？path中的stroke确定了颜色，此处可以变更为条件显示，下方波浪线示例为大于100%青绿色，否则红色。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6RWU51CdguFsT15rWKicYMwULDzZLzQ678ekvLnEU5Jh4SEnW3a9pIrx7Ws9Hl5QXSxBC1FJRf93Ig/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RWU51CdguFsT15rWKicYMwU41sibcGibm3SffWAb4DYH3ZwSwzeLFwAzvqmrQO5CsQdx4EyePNJBtpQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

除了在表格直接显示，也可以用到条件格式图标，比如前期讲过条件格式排名，外框比较方方正正。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6THILtm72DTqehRUwicJQ6pdJnVTWiacmUyUQNlAK9xbBgMnW3ibibibxCpm8T5SZmp29H5pMqXTlTJic6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

现在可以涂鸦式：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TSb8BVeGl1iaU1xyCA2moTxBqSGALC2ueEfUsZQoLygvRnUaL0EL83RljibQ28tibAWmD3KYofGuzWA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

本文配套pbix文件及视频教程在下方知识星球提供，直达连接 

_https://t.zsxq.com/09ckkFcaD_  

___

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6SrFOpSISmqT2k74QM76UrbIBKw9vBMzBUmBfibKCas2iccpABJdicQ4UNYGL2QCMLGaesXVyJ601kvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

[详情介绍](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491267&idx=1&sn=9f8011a4c2a7f38f17b6ef4168625c63&chksm=97db2793a0acae853c07277e58d55c0b8db67e953b44228508b7282f4e907af330cf64efbf51&scene=21#wechat_redirect)
