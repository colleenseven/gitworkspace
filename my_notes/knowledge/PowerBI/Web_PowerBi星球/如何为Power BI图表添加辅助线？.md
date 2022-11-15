---
notes: True
aliases: null
create_date: 2022-08-15T12:23:03 (UTC +08:00)
tags: wx/pbi/可视化图表
pagetitle: 如何为Power BI图表添加辅助线？
source: https://mp.weixin.qq.com/s/9TavAQ1EK77YfKxljmYNvg
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

DAX:: AVERAGEX, ALL

---

辅助线是可视化的一部分，是对图表的必要补充，为图表添加合适的辅助线会让信息看起来更清晰直观。  

辅助线有多种形式，比如<mark style="background: #FF5582A6;">平均值线、最大值线、最小值线</mark>等，在PowerBI中，<mark style="background: #FF5582A6;">添加辅助线一般是通过图表的分析功能来实现</mark>的。  

选中需要添加辅助线的图表（以下面这个柱形图为例），然后点击右侧的分析按钮，就能在里面看到支持该图表的各种辅助线。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPavjY3lPGForcyWNmqZO5nJIVK7sTqL0v3rDayicibcQTeXFMT1r1wAHyQBkIZzb9q8S8OyCszajkQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想在这个柱形图中添加一个平均值线，就可以打开平均值线的选项，添加一条线，并且可以自定义该辅助线的的显示样式。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPavjY3lPGForcyWNmqZO5ntAicOEY13Uz5h6ydDyN96E4dDHhlmvKGYmbJQchap2hbDOqc85jibxiag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

添加均线以后，就可以更直观看出哪些产品的数据超过平均水平，哪些低于平均水平。  

添加辅助线就是个很简单的功能，关键在于灵活运用，之前分享过的很多可视化案例都有用到辅助线。比如在<mark style="background: #FF5582A6;">关联分析中，对散点图添加x轴和y轴均线，就相当于一个四象限图。</mark>

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPMPdM3A09z3t8qjkeKibMjFznlCWZZnSJHeVlxrd2LJ15QmKRS5yHLLrfrVxgXJHf26RoSZu54ibuA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

参考：[如何用Power BI分析产品关联度？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068422&idx=1&sn=218b3a331f4ea648d4c3e2d0e05701e4&chksm=8e0c4a91b97bc387219523f5ae09fa32e60a8c04b3d02bbdc2763bd6e72ae09f32f1ee1b4e7d&scene=21#wechat_redirect)  

在<mark style="background: #FF5582A6;">盈亏平衡分析中，盈亏平衡点的垂直交叉线是利用x轴和y轴恒线来实现</mark>的：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMdLcDZj9oMDDzaIvqXibV2lYASicpAOWiaepIA0uvx7H3zXFh1hS0SEDaF0Xos6tdcVuOs6sat8kcgg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

参考：[Power BI盈亏平衡分析-优化](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

还有<mark style="background: #FF5582A6;">用阴影来突出显示特定日期的案例，是通过添加误差线来实现</mark>的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPtJqPCmPPTn0EC7W4Oz6kZeVISzFgPPHrt6DAJapt5G1hRqtAk2NoEV3lMvkQ07wqadbCyzxqVUA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参考：[利用Power BI的误差线突出标识特定数据](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080740&idx=1&sn=35d79fe9b07ef220758b30b87824d3da&chksm=8e13bab3b96433a5ffd300747ed6c1fc8b8711a7167a90a91a44f5776cdd3ab16022f37bf057&scene=21#wechat_redirect)  

在分析面板添加辅助线的功能并不支持所有的图表，添加辅助线同样遵循每个图表的可视化逻辑，比如地图一般不会需要添加辅助线，所以地图中的分析面板不适用。

即使是支持添加辅助线的图表，不同的图表之间也有区别，比如折线和簇状柱形图，目前只支持添加误差线。 

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPavjY3lPGForcyWNmqZO5n9DteOKYxrIgaqHwuIseK2ibXItUheDz9aXSYuQc7W6Pd0CXQAmhBh6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想在这个图表中添加一条<mark style="background: #FF5582A6;">平均利润率的辅助线</mark>，怎么才能实现呢？

既然无法通过分析面板直接加，可以试试通过图表本身的元素来变通实现，上面的需求可以用度量值计算出这个均值：  

> 平均利润率 = 
> 
> AVERAGEX(ALL('产品'\[产品名称\]),\[利润率\])

将这个度量值也放到组合图的【行y轴】中，就可以实现平均值辅助线的效果。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJObiasxnicSjd7UArft4Y463q7ZwvhNakl3XZa2ibt9G0eSEricIRLCXGbRxsBBp1JDxWVJ0982cakzhQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
