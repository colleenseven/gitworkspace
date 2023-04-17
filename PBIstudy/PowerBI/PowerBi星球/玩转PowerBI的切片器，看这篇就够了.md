---
create_date: 2021-01-26T20:19:59 (UTC +08:00)
tags:
aliases:
pagetitle: 玩转PowerBI的切片器，看这篇就够了
source: https://mp.weixin.qq.com/s/CuXn0A4NNdwVIbryBl9qaQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

切片器作为最常用的控件，大家都不陌生，它很简单，拖入一个字段即可使用，但也有很多人不知道的小技巧，熟练掌握它的各项设置可以帮我们更好更高效的设计报表，本文就介绍几个最常用的设置。  

**1、切片器样式**

默认的文本切片器样式是“列表”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNEon7dlL6fcjP1z8O9gNd3OPhoicOhhjibibwKQ6JSt1Ec7NF2eAM1FlEp9mDA9eRT8CiabeqOIKYkSg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有不少人问过，如何将这种切片器改为按钮式的，其实只需要在格式面板中，常规>方向，改为“水平”即可实现：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNEon7dlL6fcjP1z8O9gNd3abYxJcycy6Qb9V1NesDTbibKhEpgH3oSCRTz46YMolCuP5PgeMLOFlQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

对于数值型字段的切片器，默认的样式是“介于”，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNEon7dlL6fcjP1z8O9gNd33jgfNib4gvXnNCWZ59fZ9W9tXfSXlibtDRMuqHATAHyicTibZiao9VKicmRA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果不喜欢这种样式，依然可以改成按钮的样式，先点击右上角的下拉箭头，改为“列表”，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNEon7dlL6fcjP1z8O9gNd33sgicS5ad1XP1w0yCWnl73hNfjjlkp2bDc4hZgjybiacNqictoNb9hhQw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后按照上述方式将方向设为“水平”就可以了。

如果找不到向下的箭头，请在格式面板中打开“切片器标头”。

样式中还有个下拉式切片器，也很常用：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNEon7dlL6fcjP1z8O9gNd3gP5jvNkKTanHu8x4tWiawfXUWlX98ibN1L98pqZ88mFPqicibasiaKKia7FA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

关于切片器的样式，基本就是上面几种，对于日期型字段的切片器，更丰富一些，参考：[利用PowerBI的日期切片器，轻松搞定时间序列分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067743&idx=1&sn=018c56e68a180036951e0ba4f6570171&chksm=8e0c7748b97bfe5e9778d149687ec01ef4117134e0a0a3391a27a8f019044d457397d5ce631f&scene=21#wechat_redirect)

**2、切片器的搜索**

如果字段的数据较多，列表中一个个找太麻烦了，这时可以打开切片器的搜索功能，快速帮你定位需要的选项。

点击右上角三点>搜索：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNEon7dlL6fcjP1z8O9gNd3icgksss6sZcNqMC0JicTlxnO7NpUSq4bnPDFXOtVGwuicvuPm08ktukow/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**3、切片器的层级**

切片器不是只能用一个字段筛选，还可以将有层级的几个字段都放进来，形成一个带层次的切片器：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNEon7dlL6fcjP1z8O9gNd3U2ygRf1V7NiaYc83dvKAuCxQMJPMf5mNWicGOPkiciaBicOxhuBrI1d4icAQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**4、切片器的单选/多选**

切片器可以强制单选，也可以多选，这些都是在“选择控件“中设置的，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNEon7dlL6fcjP1z8O9gNd32lyEJ7CeAMiaR6DUSA06jicXwX4lNUjQSx4NNrZlLzvyeH2bsqBJW3zQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关闭单向选择，就是允许多选，默认是按住Ctrl键进行多选，不过**如果设置有移动布局，建议将该项关掉，因为在移动端交互报表时，是无法使用Ctrl键的。**

关掉Ctrl多选以后，可以直接通过点击某个选项来选择或者取消选择。

**5、切片器同步**

切片器不仅能控制本页的图表，还可以跨页面使用，这就是同步切片器，结合这个功能，可以灵活的设计页面导航，具体做法参考同步切片器的介绍：[灵活使用PowerBI的同步切片器](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068670&idx=1&sn=c3058974e1651626ff2a80a318e6e7da&chksm=8e0c4be9b97bc2ff1cccdb26a04e84534eb3c129776ef26e71c99459ab57e54c006debfb3b2c&scene=21#wechat_redirect)

**6，切片器的颜色、形状**

PowerBI内置的切片器，对于颜色和形状的设置非常简约，可以调整但也只是点到为止，个性化调整有限，如果想实现更丰富的外观设置，可以使用自定义控件Chiclet Slicer，参考：[利用PowerBI的这个控件，美化你的切片器](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073642&idx=1&sn=d4e57071dc6421b4bb2f0bc9fc1e51b2&chksm=8e0c5e7db97bd76b1e9de73326a5676b2b5aeca519c036bbc9a30ee7a15075145783e09c55b8&scene=21#wechat_redirect)  

关于切片器的格式设置大抵就是上面这些，关键是要动手熟练掌握，然后在设计时才能得心应手。

在功能上，切片器默认的就是直接筛选，选择什么显示什么，如果想改变默认方式，还可以利用DAX实现更多个性的交互方式，参考：

[利用DAX，突破切片器的默认交互方式](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072463&idx=1&sn=95c684b48ff2e2779ca90f734688b3e1&chksm=8e0c5ad8b97bd3ce897a72e1255398769c1a0da914a553dab6f39d34f9cf4e8169bb1a97f96a&scene=21#wechat_redirect)  

[PowerBI切片器，原来还可以这样交互？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074281&idx=1&sn=ea825a10f8bb56815772997dcccfff08&chksm=8e0c5dfeb97bd4e8b6bf810457b5c579cf6633545260ce2097d21bc48e187bd88f49f3c528bf&scene=21#wechat_redirect)  

___

**PowerBI星球的**[**历史精华文章合辑**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)**：**  

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNn5eia186067w5or6WoVmwdm210CYQfaibhdzFvJvR59sFUgk13iauEzR4oLzGvXiaziaX8VJcB2sCbzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

___

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和 3k+ 学习者一起成长
