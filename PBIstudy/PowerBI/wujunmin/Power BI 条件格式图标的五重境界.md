---
create_date: 2023-01-0700:06:22 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 条件格式图标的五重境界
source: https://mp.weixin.qq.com/s/yjdRgIxHkoJClpGbGCvs4Q
author: wujunmin
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

这是一篇自定义条件格式总结，其他总结

[_零售书籍Top10-2022版_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491268&idx=1&sn=4135f38418c1912e6c13c4d09decc1df&chksm=97db2794a0acae82629ec6c7a193068c07a549893063d021c061aa6187fef7f206ee3aa8d1eb&scene=21#wechat_redirect)  

[_Power BI模拟大厂图表总结贴-2022版_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491403&idx=1&sn=b868c0fc4b935aaba5f3490533cfb5c9&chksm=97db261ba0acaf0d717007b39c83e1dfa5a6a995bc1abaf778faa15981ec11139a4fd8b291b6&scene=21#wechat_redirect)

[_Power BI SVG地图应用总结-2022版_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491530&idx=1&sn=f33aea046bf8259f87f75d6bc2b2b30e&chksm=97db269aa0acaf8c3c7827f81d3a551d12d2f310d6bae9f257fbdf72b29ced78869c5b8fcc44&scene=21#wechat_redirect)  

___

Power BI的条件格式有五种模式，背景色、字体颜色、数据条、图标和Web URL。在这五种模式中，只有条件图标可以有无限的扩展性，其它四种功能比较单一。条件格式图标可以怎么玩？下面以五重境界进行描述。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6TQccroicyKleJOpvjrpHpThU3Q2r8GKFyya5e6em8DrNA3vtrQPgvkZheHGU1jFNf0FCOCUgTYyVw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

_下方示例为[知识星球会员](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491555&idx=1&sn=938fc2d95536402d9eddf5bf45e2a3a1&chksm=97db26b3a0acafa5e88ff6afe782031937a6023e5c46ea6e04e64c76dfc699963b302a978d7f&scene=21#wechat_redirect)提供pbix源文件_

**第一重：内置图标**

___

条件格式图标最基本的用法是使用内置图标，Power BI提供了若干图标选项，可以为数据设置对应条件。  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

下图为业绩达成率设置了不同的内置图标：  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

**第二重：自定义图标**

___

内置图标不满意，则有使用外部图标的需求，比如同样是红绿灯，内置红绿灯不能修改大小，也不能修改颜色，更不能空心，《[Power BI 条件格式红绿灯图标修改](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247490532&idx=1&sn=ee9de270d8532186be414f4c67623129&chksm=97db22b4a0acaba23cf79af30b71505aa294023e62ff55653fe84891b3871bfc47ff943c0b0e&scene=21#wechat_redirect)》这篇文章给出了修改方法。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QEHcXDnibFte03eEhW6ibYHnj4rHHYcibMv5hZPTkOS3jKmD9ichT0md3Xt7Xkwh41HhpZLPVmpu2XWw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QEHcXDnibFte03eEhW6ibYHniaWn2Z3fEz4BZuXhgm2VH187n8dAxNEJlHB9SIowib32bKd46ibfeX7TQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_本文示例pbix：https://t.zsxq.com/09YLAxEKJ_

条件格式图标可以看作一个图片，条件格式图标支持多种形式的图片，比如URL，BASE64，SVG，对于表格矩阵的图片支持可参考此文《[Power BI表格显示图片的若干问题](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491377&idx=1&sn=31c43037a6808cae193a2a09e64b4b77&chksm=97db2661a0acaf7769ee4b8d825deb646e18a7811d224821b07c92c2a519528f97f107325c0d&scene=21#wechat_redirect)》

PNG和SVG的方式可以参考此文《[Power BI自定义表格图标条件格式：以服饰品牌2022价值榜为例》](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488892&idx=1&sn=7dd82b87553e3c458aaa2046a7b61d59&chksm=97db2c2ca0aca53a2939bd757e8cff165ffb9900acbd559f7f049603983dc64c6dae49e5dff1&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QxQXS6w13SiaACF5EicjhIkPJwDHp0iccQBgYEjKol4n4wayTrF6cfm4ZbfeibibysF4D03LzKRvFMqaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_本例pbix下载：https://t.zsxq.com/09a0geZPV_

以下是产品资料带有BASE64图片，可以将产品图片显示在条件格式，这和PNG、SVG操作没什么不同。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QQkGLgBrD7xBuqvbrwTZ5NUpGWUbKjEJKOOcHQ4icDDbN4yOr1FyoPLxBZrSCicuaukZa805mkQ6lg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QQkGLgBrD7xBuqvbrwTZ5NfBSiaQkz4eLKqnZgNb8wtPdjsvhZca9JtX0w5M1llIgRlXOq1gf35nQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_本例pbix下载：https://t.zsxq.com/09AJAPalQ_

**第三重：字段图标融合**

___

前面两重可以看到条件格式图标与字段值（比如产品图片和产品ID）是独立存在的，二者也可以融合为一体，产生一些实用的效果。

[《Power BI同一数据显示不同单位](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488999&idx=1&sn=5628e6d6be32c1d0880b9544b4cfbd61&chksm=97db2cb7a0aca5a117f33e20d728e51f5dfb0db2eb27baa77504d9637d69299bdae00e178b2b&scene=21#wechat_redirect)》这篇文章巧妙的利用条件格式图标显示了数据单位。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Qsz51UA3GOTP0jcV08Bicdib6SWxPkPELKibAtA8JCdufMaJ2QwkcQQDgM3jbmeEWRgJ5Q0aMnGOa7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_本例pbix下载：https://t.zsxq.com/09FuY2rDu_

《[如何将假日安排植入Power BI日历?](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491281&idx=1&sn=0ebecc40154c8ec5f2cebc7ece988665&chksm=97db2781a0acae9751a470ce1eb3b94cef7bfc8ad219648e8d5237bccabdb115d0b7a8622113&scene=21#wechat_redirect)》介绍了公历和农历、假日融合的例子。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6St9GLicicic6tdRBjuwpNHicljURa6yPdWf7kDGlYfGDZ4gcbryDsba9vIYzaKGLtl0V79vPicJB8ywXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6St9GLicicic6tdRBjuwpNHicljYRGHeJic206GLxsm7Zy0s64XlQWTSSrWVn2SGYV9vwL0QkwIu1qOkjA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_本例pbix下载https://t.zsxq.com/09OkYQAPB_

**第四重：图标数据化**

___

条件格式图标可以依据数据被改造，从而提高信息密度。《[Power BI条件格式：排名四招](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247490550&idx=1&sn=6a278b0194e37113d34bb2b290bfa180&chksm=97db22a6a0acabb0a70ad08189a2a77f52a7580a3b8bf522a1f7db54f35143df9406dc918c7e&scene=21#wechat_redirect)》利用条件格式将指标和排名放在一列，大大节约了画布空间。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TQccroicyKleJOpvjrpHpThISBzG4c5ZBnEULndYb071GB4dibQXJ8boP7ybOibZxeeDPlL5aNp4msQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_本例pbix下载：https://t.zsxq.com/09wwq6pmP_

除了排名，其它简单的指标图表也可放在条件格式，比如百分比：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TQccroicyKleJOpvjrpHpThAPJjibTOamTQ2M9LEZ7RMYvvs1PfYuAByIoP2xhibHauDxwN2nWWnLyQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_本例pbix下载：https://t.zsxq.com/09lP3Zorg_

**第五重：串联图标**  

___

以上四种模式，上面一行图标和下面一行没有关联，通过一些手段，可以突破表格行限制，将它们串联起来，产生更加丰富的可视化效果。《[Power BI 优化表格矩阵中的条形图](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491125&idx=1&sn=9331faf4949d44e67a61827e45671d2b&chksm=97db2765a0acae7307b1eb3b7a439a62698880019bf2586bd933fed6a7e5e61a37db60ebf3bd&scene=21#wechat_redirect)》介绍了条件格式图标制作条形图、大头针图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RTKonOccmzOhEJ0dvEyavkibz3Dr6kxfIhiclD5rbHBnxTupibXxJYPpc3tcibQTqoibkR6UUeNGJfdbg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)  

_本例pbix下载：https://t.zsxq.com/09OydVPQ4_

《[Power BI窗口函数应用于图表设计](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491348&idx=1&sn=d457df1d8a24ed4d83b5b1bc2f25516c&chksm=97db2644a0acaf52ba7a522ead1495e18e7d370b39beeb463660e81239a50645fbc92dec833a&scene=21#wechat_redirect)》更为夸张，制作了纵向折线图，上下图标无缝连接。

  
![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Ro5z9o7jVFn9TibTjRqNgrWpOEtZkgbreqb8Fvjjg2GAqo83sNTVZiaEmkqFZib4lXdPKGjsvuIX7Xw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

_本例pbix下载：https://t.zsxq.com/09PlAsPkz_

条件格式图标占据如此狭小的空间却可以产生如此丰富的可视化效果，后期本公众号还有更多介绍，敬请期待。  

___

  
加入知识星球，享有90+节视频课程，200+源文件，详情介绍：[Power BI业务实战及图表开发社群&视频课程](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491555&idx=1&sn=938fc2d95536402d9eddf5bf45e2a3a1&chksm=97db26b3a0acafa5e88ff6afe782031937a6023e5c46ea6e04e64c76dfc699963b302a978d7f&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6SrFOpSISmqT2k74QM76UrbIBKw9vBMzBUmBfibKCas2iccpABJdicQ4UNYGL2QCMLGaesXVyJ601kvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
