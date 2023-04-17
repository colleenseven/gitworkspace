---
create_date: 2017-12-22T20:48:33 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases:
pagetitle: 体验Power BI | 分分钟生成一份可视化图表
source: https://mp.weixin.qq.com/s/x3h326DGcLxlWKM8qlSWpA
author: PowerBI星球
status: 已完成 
category: 浏览文章 
notes: false
ZK: Origin
uid:
---

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0pC8YeOun7MQ7zNCRzmOMMZDIwtiahRbzxFmib6BwNXhLwhrKrb8sxa6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 微软宣称Power BI只要几分钟就可以将数据转化为精美的图表，要不要尝试一下？

___

首先我们准备一份数据，Excel格式  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0lwomzgbic6VjFFhCylskoA5wJmicE7F8vY7yEsvu29k6qib9EBpYU6Zsw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

数据是从2006年到2015年10年间，中国大陆31个省市的三个产业的GDP,我们用Power BI来看看这三个产业结构近年来有什么趋势？

首先第一步，获取数据，选择Excel格式导入：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z029slAEfcSch7p26czSYCnJDtMgDMRn3pBgnjHFP2ticP1xIJVx9QO5A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里选择编辑，进入查询编辑器，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0RZBVwqaI833HvJtzM5was7wtKfS3Mz6OfCJiatoXMTjUVr2J9uqUSRQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个表格是二维表，为了分析的方便，需要把二维表转化为一维表，这个操作在Power BI里非常简单，这里把三个产业结构的数据转化为一个字段，选中地区和年度列，从转换里找到逆透视其他列：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0ibhIYzdZJjYwTia2jzLrUDgntQ1RZ2Uos2KlrkOTwyT9xXSZWNlfwa6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就成了一维表了，把最后两列的名称重命名一下，点击关闭并应用：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z02Vg6W4UFnLqaA9iafP2fanBSAG0rK5LZ5ZEJjMjcuibTiaxyCBcuHibTTw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

数据上载后，就可以在字段区看到这张表的字段，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0Kq7lGc1NdTMEYzLwtcxEkyyFWsGvPxlDQsicqYiciayjgzvoibf4uN6yvw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

到这里数据已经整理完成，开始生成图表。  

为了直观看出各个产业的数据，我们先做一个产业结构数据的矩阵表：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0g2pbZ9obCVZGyMUs4XD8zTsyCEjfTfiaM1bgiaVpR6J7ptUhhqSaMxtQ/0?wx_fmt=gif&wxfrom=5&wx_lazy=1)

是不是很简单，就是把相应的字段拖进图表编辑框中而已，然后同样拖拽字段生成圆环图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0SywZ9IPKtB2FI6hnOiaMVtH820lUxtV7DDVDaIBoqX5yiauFF1L9pZSw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这两个表都是按产业结构分类的，并没有把年度指标考虑进来，下面就来看看如何把年度放进来：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0uymkMWhHhWBQwr70icSYb5zeTKib1ZWwibB4ChNQzwmUdxj8wl49QTtMQ/0?wx_fmt=gif&wxfrom=5&wx_lazy=1)

实际上是做了一个切片器，通过点击年份的切片就可以控制另外两个图表的数据，这就是图表间的交互功能，我们先看一下效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0RVibork4WEsoYxcbKVGZT90s3Ald6sygkaRtXoWCaiaragKW7nGDrTFA/0?wx_fmt=gif&wxfrom=5&wx_lazy=1)

不仅要看每年的数据，还想看这十年来的趋势，那么就放个堆积面积图：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0pj7G3ZmsibZ6Ky0NfOXMhuYQ1aDAvtcCG0f0S7QtA4QesdgkMGSQ36A/0?wx_fmt=gif&wxfrom=5&wx_lazy=1)

从这里可以看出GDP的增长主要来自于第二产业和第三产业规模的扩大，第一产业的规模基本没什么变化，占比逐年降低。

原始数据是大陆31个省市的产业数据，到现在为止还没有把省份纬度放进来。和刚才的年度切片器一样，再根据地区做一个各省市的切片器，然后在画布上拖拽调整对齐这几个图表的位置，并在上方写个标题，这套图表就完成了，我们来看一下效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0PFpk9nicQFBtqb211NwuS928RUDqNhmrah0zLfBTzneUVeDRcn1iclmg/0?wx_fmt=gif&wxfrom=5&wx_lazy=1)

是不是很快，如果操作熟练，5分钟左右就可以生成这样一个可视化图表，微软所言果然不虚。这个图表虽然看起来还有很多地方需要进一步完善，但这个效果已经超过大部分人用传统做法耗费一两个小时的成果。

至此，我们体验了PowerBI把数据通过简单点击几下鼠标就生成图表的整套流程，这速度简直要上天了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0ZRSELWzVBicwkv82kZwKM5icJFpSEJSTPyvicPEgnc0ZP99tRpT3cFWFw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Power BI还不止于此，这个图表我们还可以进一步分享给其他人查看，点击发布，将该图表发布到PowerBI网页版，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0jLKUgqaiciaZk8MA8kdhOQHxlo44CDahXZwmWVfXiabqXCNVmiaS2M4dmg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后在网页版中选择发布到web：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0icx2Q0icnBXpMV5cZo9SqAXIovictoEiaZxvrPCfHic45ibDRfibMKhzean8w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

就会生成一串网址，把这个网址发给接收的人员，他们就可以随时随地、通过手机平板都可以查看这个报表了，并且这个报表不是静态的，也是可以点击交互的，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPzG47fbibPJ06HTicicP333Z0j4OGn6WaRwn6LtSMLVu6UbbF7tYtav4cfBY6GVjRjBQ2Bqnt1liaicrg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这份图表的网址如下，也可以点击阅读原文查看：

https://app.powerbi.com/view?r=eyJrIjoiMWFjMGM4ZTctNTQ3Yy00YTg2LWJhMjItNmVmMzA4NGZiMTI4IiwidCI6ImUxMTAyMjkxLTNkYzUtNDA1OC1iMDc3LWQ0YzU4YWJkMWRkOCIsImMiOjEwfQ%3D%3D

看到这里感觉PowerBI怎么样，是不是有种相见恨晚的感觉呢，无需感慨，更重要的是马上动手开始做。原始数据我放在百度网盘里了，点击下载即可练习：https://pan.baidu.com/s/1eSdFqMI 密码：t6xt。
