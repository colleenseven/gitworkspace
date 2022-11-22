---
ZK: Origin
create_date: 2022-11-04T12:40:20 (UTC +08:00)
tags: wx/pbi/建模技巧
aliases: null
pagetitle: 如何在Power BI中计算和展示时间进度？
source: https://mp.weixin.qq.com/s/4A-lCTrydJjUcLbj_DLudQ
author: 采悟
status: 已完成
category: 精读文章
notes: True
uid: 
---

DAX:: DIVIDE, DAY,TODAY,EOMONTH,STARTOFQUARTER , TREATAS, ENDOFQUARTER, STARTOFYEAR, ENDOFYEAR,SELECTEDVALUE

经常有人问到在PowerBI中如何展现时间进度，这里就以今天在本月、本季、本年的时间进度为例，来看看如何用DAX函数进行这种计算，以及用可视化的方式展现出来。  

今天在<mark style="background: #FF5582A6;">本月的时间进度</mark>，就是<mark style="background: #FF5582A6;">今天是本月的第几天除以本月的天数</mark>，度量值可以这样写：  

> 本月时间进度 =
> 
> DIVIDE(
> 
>     DAY(TODAY()),
> 
>     DAY(EOMONTH(TODAY(),0))
> 
> )

这里<mark style="background: #FF5582A6;">DAY(TODAY())返回日序号</mark>，也就是今天是本月的第几天；<mark style="background: #FF5582A6;">EOMONTH(TODAY(),0)返回本月的最后一天</mark>，然后利用DAY函数，计算月末最后一天是第几天，也就是本月的天数，二者相除，就是本月时间进度。

上面的逻辑很容易理解，而对于计算<mark style="background: #FF5582A6;">今天在本季度的时间进度</mark>，会稍微麻烦一点点，需要计算出<mark style="background: #FF5582A6;">今天距离本季度第一天的间隔</mark>，以及<mark style="background: #FF5582A6;">本季度的总天数</mark>，依然可以按照这样的逻辑，分步计算出这几个天数。

这种计算可以有很多种写法，这里我用时间智能函数来实现季度进度的计算：

> 本季时间进度 =
> 
> VAR A=STARTOFQUARTER( TREATAS({TODAY()},'日期表'\[日期\]) )
> 
> VAR B=ENDOFQUARTER( TREATAS({TODAY()},'日期表'\[日期\]) )
> 
> RETURN
> 
> DIVIDE(TODAY()-A+1,B-A+1)

这里利用了两个智能函数，<mark style="background: #FF5582A6;">STARTOFQUARTER和ENDOFQUARTER来返回本季度的第一天和最后一天</mark>，由于时间智能函数需要使用<mark style="background: #FF5582A6;">日期表的日期作为参数，所以这个公式利用TREATAS将TODAY视同为日期表里的日期</mark>，作为参数，同时也将<mark style="background: #FF5582A6;">TODAY作为上下文，来计算TODAY所在季度的第一天（A）和最后一天（B）</mark>。

然后<mark style="background: #FF5582A6;">TODAY()-A+1就是TODAY在本季度已经经过的天数，B-A+1是本季度的总天数</mark>，二者相除就是本季度的时间进度。  

这个写法同样适用于本月时间进度和本年时间进度的计算，比如本年时间季度，<mark style="background: #FF5582A6;">只需将时间智能函数替换为STARTOFYEAR和ENDOFYEAR</mark>：

> 本年时间进度 =
> 
> VAR A=STARTOFYEAR( TREATAS({TODAY()},'日期表'\[日期\]) )
> 
> VAR B=ENDOFYEAR( TREATAS({TODAY()},'日期表'\[日期\]) )
> 
> RETURN
> 
> DIVIDE(TODAY()-A+1,B-A+1)

这样就实现了TODAY在本月、本季和本年的时间进度，如果你想用切片器任选一个日期，来查看该日期的时间进度，你可以<mark style="background: #FF5582A6;">将上述公式中的TODAY（）换成SELECTEDVALUE('日期表'\[日期\])</mark>就可以了。

上面的这几个时间进度计算，关键是熟悉并灵活运用日期函数和时间智能函数的用法。

时间进度数据计算出来了，那么如何直观地展示出来呢？通常可以用个卡片图直线显示进度数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaPQAWiaAzNrvlWCkInJoTp88sGLE75r6iaScrSMwMZpWs0pOklwS3r6Nauk9ybGIGiaYBpoOIrwaGA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当然还可以用可视化图表的方式来更美观的展示出来，比如对于本月时间进度，再写个度量值：  

> 本月剩余进度 \= 1-\[本月时间进度\]

然后将本月时间进度、本月剩余进度两个度量值放到环形图的值中，就可以做出环形进度条的效果。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaPQAWiaAzNrvlWCkInJoTpa8aBWvj4YUQIlqYTsBk9v8zJqdWtq0ZXKjF3c3IvjAKlo0icbr3NsSw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还可以在环形图的中央放个文本框来显示环形图代表的含义，以及动态进度数据（文本框中插入度量值的方法可参考：[利用Power BI智能叙述，生成动态报告摘要](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073801&idx=1&sn=3a6dcd73ed52e77a4159612fe49af3e7&chksm=8e0c5f9eb97bd68889ce7e6ae0af81e62b7ed6b7ea7827deb5ca1ba097c14e4965889736baa4&scene=21#wechat_redirect)）：

这种显示效果是不是更棒呢？

同样的方式，可以制作本季时间进度和本年时间进度的可视化效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMiaPQAWiaAzNrvlWCkInJoTp1HxWrBetEXvwh6Gdm7fSBmwj8wZKoD2JBibLUn89PAjROibdIuUFnrxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于时间进度的计算和展现就介绍到这里，希望对你有所帮助。
