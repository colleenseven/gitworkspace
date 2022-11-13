---
create_date: 2021-10-24T12:58:39 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何利用Power BI原生图表制作甘特图？
source: https://mp.weixin.qq.com/s/i1EbzThV7m5E68Au0rBhzA
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

在做项目管理时，经常会用到甘特图，之前分享过一个PowerBI制作甘特图的做法（[使用PowerBI制作甘特图](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067594&idx=1&sn=ccf72caedaee572b20e75740b92ba8c0&chksm=8e0c77ddb97bfecb4a982a614f02c377a01a627e6624266fa73fd4ce52af84875b8cddabfa88&scene=21#wechat_redirect)），是利用自定义图表实现的。

自定义图表无论是性能、灵活性还是兼容性上，一般都不如内置原生的图表，所以这里尝试用内置的堆积条形图来模拟制作甘特图。

以下面这个数据为例，记录了每个项目的起止日期：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNxQ2JZquKhpmqqGGAXfh3TJeWsqr0XB6GEYG37yqZDACbQiafLPHumjGBgoTvDiaKLe4Pn6IjeB3icA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

甘特图的作图原理，其实就是用Y轴区分项目，X轴显示每个项目的日期范围，所以非常适合用条形图来制作。

为了让条形图的每个条从相同的日期开始，先计算所有项目中最早的开始日期：

> 最早日期 = MINX(ALL('项目表'),'项目表'\[开始日期\])

每个项目的开始日期，距离这个最早日期的天数，填充在堆积柱形图左侧条，这个天数可以这样写：

> 左侧填充 = INT(MAX('项目表'\[开始日期\])-\[最早日期\])

然后利用项目名称、持续天数以及上面建的这个度量值，制作一个堆积条形图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNxQ2JZquKhpmqqGGAXfh3TAzjV2SLVjRIlseBgAsbcC22o6ibpCMuD5aFe4nwAia9GricGx0madAldA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后将左侧填充柱形的颜色设置为与背景一致，就得到下面的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNxQ2JZquKhpmqqGGAXfh3TZXv4mevwG7s4S7Yt7ZlBThc3ficpdnXA97zlHicrchuIvuxRcNRic1UZg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是一个简单的甘特图。

为了能够更直观看出哪些项目已经完成、哪些项目正在进行中等这些状态，可以将不同的项目按颜色区分开，但是上面的效果无法单独设置某个柱形的颜色，我们需要变换一下做法。

对这些不同的状态的项目天数，分别写度量值：

> 已结束 \= CALCULATE(SUM('项目表'\[持续天数\]),'项目表'\[项目状态\]="已结束")
> 
> 进行中 = CALCULATE(SUM('项目表'\[持续天数\]),'项目表'\[项目状态\]="进行中")
> 
> 已结束 = CALCULATE(SUM('项目表'\[持续天数\]),'项目表'\[项目状态\]="已结束")

然后将这三个度量值作为条形图的值，当然左侧填充的度量值也要放进去：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNxQ2JZquKhpmqqGGAXfh3TVn1Pbl7iaiaYFb8Fsqn5hUpygrTgKwtCOKpLRvnSTxTicAicpSdXJAoR1A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并设置不同的颜色显示，就可以得到这样的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNxQ2JZquKhpmqqGGAXfh3TDrHTlPgNWjokm9HXWCg8ghaSOWCEERuNE5v8ictJQ868jKUMTlKzXkQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来稍微清晰一些，但是无法直观的看出具体的日期，这些条形的长度是每个项目的持续天数，X轴也是天数，那么如何将日期标识上去呢？  

这里可以用辅助线来显示日期，当然因为X轴是天数，不可能直接用日期做辅助线，依然需要按照日期相对于项目最早日期的差额来确定，这里以显示每个月末的日期为例：

> 月份刻度1 = INT(EOMONTH(\[最早日期\],0)-\[最早日期\])

上面度量值的逻辑是，利用EOMONTH函数返回最早日期移动0月后的月末，也就是当月月末，减去最早日期，就是距离最早日期的天数。  

同理，对于这些项目期间，可以写多个度量值，将每个月的月末标识上去，

> 月份刻度2 = INT(EOMONTH(\[最早日期\],1)-\[最早日期\])
> 
> 月份刻度3 \= INT(EOMONTH(\[最早日期\],2)-\[最早日期\])
> 
> 月份刻度4 \= INT(EOMONTH(\[最早日期\],3)-\[最早日期\])

还可以计算出今日距离最早日期的天数：

> 今日刻度 \= INT(TODAY()-\[最早日期\])

然后用这些度量值为条形图添加辅助线，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNxQ2JZquKhpmqqGGAXfh3TicvIBeQRYFsIicW4AGXtQicPsOjQ7lpb3HDlFAgAvcmhROMvjlL1At1Cw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

每条辅助线的名称，修改为对应的日期，辅助线的值，选择上面建好的度量值，就可以模拟出日期刻度的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNxQ2JZquKhpmqqGGAXfh3TCy8ngYuFntHjlgXEN2FiaiboyURtYa7bRV3EZur9UQtEs2jwUwicibq64g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就能看出每个项目所处的日期范围，是不是更像是一个完整的甘特图了呢。

你也可以继续完善这个甘特图，比如添加辅助线作为甘特图的里程碑，设置工具提示显示每个项目的细节等，这里只提供个思路，不再继续深入。

以上只是一种简易的甘特图制作方案，相对于专业的甘特图作图软件，依然显得简陋。这种做法，以及PowerBI中的几个自定义的甘特图，各有不同的特点，适合不同的场景，你可以选根据需要择适合自己的。

**本文介绍的是如何用条形图模拟甘特图，需要熟练掌握条形图的各种设置技巧，但更重要的是掌握可视化的展现逻辑，不要把PowerBI的图表制作当做一个黑箱，只知道把字段拖拽进去，至于出来什么图表、为什么图表是这样展现的，以及如何调整图表的元素细节，却一脸茫然。**

其实图表制作并没有什么神秘的，关键是理解每个图表的特点，根据你的业务需要选择合适的图表，多动手，熟悉每个细节的设置，以及这些设置会对图表外观产生哪些影响，搞明白哪些地方可以调整，哪些还不能调整，才能避免在设计可视化报告时走弯路。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYCTV9SBx5LXD4kp3icA9LouW3YN2z2njBWWQzM1zia9Fbeky0fdIpNakw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和3800+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCy5RUEz1Yp2hsG1ExlG3XiaqfWPqspJ1oiaEcKjuJCKPStBaWQXO6SOew/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
