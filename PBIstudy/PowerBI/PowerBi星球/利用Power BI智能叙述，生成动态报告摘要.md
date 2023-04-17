---
create_date: 2020-11-13T23:47:45 (UTC +08:00)
tags: 
aliases: null
pagetitle: 利用Power BI智能叙述，生成动态报告摘要
source: https://mp.weixin.qq.com/s/MCZnwbKLeb1TzElrHu76Fg
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

使用PowerBI制作数据报表非常方便，但一个可视化报告，不能只有图表，在报告中制作一个摘要，对图表的重要信息进行简洁的描述，让用户有个整体的概览，是很有必要的。

在PowerBI中如何快速编写摘要呢？并且这个摘要能根据数据或者上下文的变动，自动更新，而无需手工再修改一遍。

利用PowerBI的新功能：**智能叙述**，就能帮我们快速生成可以自动更新的摘要，这是9月份新增加的功能，最近也有不少人问怎么使用，这篇文件就带你了解一下它的用法。

想用这个功能，首先确保你的版本是2020年9月之后的版本，以前的版本是没有这个功能的，并且现在它还是预览功能，所以，第一步就是在选项>预览功能中启用它。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPXeuPibaDKy3ct9PGts9R0EwS2eib7xDYNe1VRsF3u9ucibXXfyumsKGP0OZdzPkXz1Wqhszq3ibibRYw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个功能之后可能很快就会普遍可用，所以过一段时间，如果你发现这里找不到了，应该就是默认可用，不需要再到这里勾选，直接用就可以了。

启用之后，就会在可视化面板中看到智能叙述视觉对象：

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

下面就以前一段介绍的预算对比分析为例（[PowerBI预算分析：预测与预算目标差异比较](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073666&idx=1&sn=427f76eaeafb6473ade9cceb86056b96&chksm=8e0c5e15b97bd703d5b6a3cef12fc07c7f7fd0e04740366501e2c832235916417ea48df48faa&scene=21#wechat_redirect)），来介绍智能叙述的用法。

报告上的图表如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhCx8TTiczKPThfA6zfF6rwOPHicPWvAFtyFAvSVVQcg5RfEZSurzzJPUeicd4xiarTiasGmKyvTGHFeA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

只展示这样一个图表，用户很难一下理解这个图表的表达意图，下面就加入智能叙述看看是什么效果。  

点击画布的任意空白区域，然后单击“智能叙述”，就会生成一段文字：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPhCx8TTiczKPThfA6zfF6rwTau7kOwjlibaiaxZqPXFaEDFTrv8g8Uowc9IAqyhg1cz9PG3p83c3w9Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

但你会发现生成的这一段文字是英文，并且含义也莫名其妙，并不是我们想表达的意思，这到底是什么逻辑！

我也不知道它是按什么逻辑生成的这一段文字，因为它是一种AI视觉效果，只负责自动输出结果，不负责解释。面对这样的结果，是不是无可奈何。

那么这个新功能是不是对我们一点用处都没有呢？当然不是，虽然它自动生成的效果无法使用，我们还可以手动，根据需要来编辑摘要的内容。

把它自动生成的文字删除，或者直接全部删除，重新插入一个文本框，你会发现，现在的文本框也已经不是以前的文本框了，它已经变成了一个AI智能文本框，和智能叙述是一样的。

假设我们想要的摘要框架是这样的：

全年收入预算目标：XXX；截至到X年X月X日，累计实现收入XXX；

假设未来期间的同比增长率是X，预计全年实现收入XXX，与预算的差异是XXX。

其中数据部分是需要动态变动的，我们直接插入一个文本框，下面来看看主要的操作步骤。

___

输入“全年收入预算目标:”，然后点击添加值，在对话框中输入收入预算目标，就会得到数据中的全年预算目标数据691,600。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPhCx8TTiczKPThfA6zfF6rwSkRia8mfpPfv36fjZjfa09dCKHYUiaKq0libicsAx4ticHgibFhtoliaAJx4g/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

点击保存，文字摘要的效果就出来了：

全年收入预算目标：691600.

这个对话框，实际上就是PowerBI的问答功能，输入关键字，系统自动识别，并提供选项，在下拉框中选择就可以了。  

当然系统提供的选型并不是凭空冒出来的，而是数据中已经存在的列字段或者我们建好的度量值，\[收入 预算目标\]就是一个度量值。

既然是度量值，就可以根据数据的刷新或者上下文的改变来自动变换结果，并且还可以在这个对话框修改结果的格式，以及对这个值进行命名以便其他值可以引用它。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhCx8TTiczKPThfA6zfF6rwUISLXxMvDLKhvlYFj2srUeuDplSwr1iaCmic62opyEy05HunMecReQHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个对话框最上方的是常规的文本格式修改面板，鼠标选中某一段文字后，就可以在这里修改，和之前的文本框一样。

生成其他几项的步骤都类似，比如截至到业务最后日期：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPhCx8TTiczKPThfA6zfF6rwfAku8S5eic6T7vw3VRx9uJgo9mXeIkbiauic4lpW68JkA8nMsYib0mWTVA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

截至目前累计实现收入：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPhCx8TTiczKPThfA6zfF6rwDEOzpOtdhZicOJkicrtYrbDiaHg2GiaBeiap7zqDzY9qOYF4n7ztl4Vb66A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

其他几项的操作步骤都类似，不再一一演示，你需要什么数据，提前写好度量值，这里直接选择就好了。

全部需要的文字摘要做好以后，可以调整摘要的格式，以及把它摆放到报表合适的地方，上面示例生成的摘要最终效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPhCx8TTiczKPThfA6zfF6rwvmEibT8hXPYEfibic9tUXAj5ibY5PxTUA1koUADHibqaBsw9ibQTnNdCr6ibg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样用户就能一眼看出来你想表达的观点，也更容易理解图表的含义，并且这个摘要是动态的，比如按不同的增长率来预测全年目标的达成情况：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPhCx8TTiczKPThfA6zfF6rwzGdfCKfaydjYOBNkibvuQMpRRGMB6ObuC22ePyxPLxibciar6x15Xfj1Q/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

是不是非常好用。

这是一项了不起的功能，它不仅可以节省制作报告的时间，而且还可以自定义数据洞察来辅助数据分析，让用户更快速的捕捉到关键信息。

虽然是智能叙述，但上面的例子其实是自己动手做的一份动态摘要，和智能还扯不上关系，期待它的AI功能越来越强大，以及尽快推出中文版，也许真的有一天，它自动生成的智能叙事正是我们所需要的，这一天，可能不会太久。

___

**PowerBI星球学习社群**  

**双11限时优惠活动进行中**

**现在加入，立减50，最后两天时间，感兴趣的朋友，不要错过这次机会哦。**

**早点加入，成长先人一步~**

 长按扫码、立抢50元优惠 

▼

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMMvf7Fad2ibaic1LIQ3DCvlFaEggvCQpR6icObWFIE21Ef7jZEUzuQt3FVZYoxzUxmdxo2q506oDWBg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
