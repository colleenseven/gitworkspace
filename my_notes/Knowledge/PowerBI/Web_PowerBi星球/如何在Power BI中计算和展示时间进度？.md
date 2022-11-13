---
create_date: 2022-11-04T12:40:20 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何在Power BI中计算和展示时间进度？
source: https://mp.weixin.qq.com/s/4A-lCTrydJjUcLbj_DLudQ
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

经常有人问到在PowerBI中如何展现时间进度，这里就以今天在本月、本季、本年的时间进度为例，来看看如何用DAX函数进行这种计算，以及用可视化的方式展现出来。  

今天在本月的时间进度，就是今天是本月的第几天除以本月的天数，度量值可以这样写：  

> 本月时间进度 =
> 
> DIVIDE(
> 
>     DAY(TODAY()),
> 
>     DAY(EOMONTH(TODAY(),0))
> 
> )

这里DAY(TODAY())返回日序号，也就是今天是本月的第几天；EOMONTH(TODAY(),0)返回本月的最后一天，然后利用DAY函数，计算月末最后一天是第几天，也就是本月的天数，二者相除，就是本月时间进度。

上面的逻辑很容易理解，而对于计算今天在本季度的时间进度，会稍微麻烦一点点，需要计算出今天距离本季度第一天的间隔，以及本季度的总天数，依然可以按照这样的逻辑，分步计算出这几个天数。

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

这里利用了两个智能函数，STARTOFQUARTER和ENDOFQUARTER来返回本季度的第一天和最后一天，由于时间智能函数需要使用日期表的日期作为参数，所以这个公式利用TREATAS将TODAY视同为日期表里的日期，作为参数，同时也将TODAY作为上下文，来计算TODAY所在季度的第一天（A）和最后一天（B）。

然后TODAY()-A+1就是TODAY在本季度已经经过的天数，B-A+1是本季度的总天数，二者相除就是本季度的时间进度。  

这个写法同样适用于本月时间进度和本年时间进度的计算，比如本年时间季度，只需将时间智能函数替换为STARTOFYEAR和ENDOFYEAR：

> 本年时间进度 =
> 
> VAR A=STARTOFYEAR( TREATAS({TODAY()},'日期表'\[日期\]) )
> 
> VAR B=ENDOFYEAR( TREATAS({TODAY()},'日期表'\[日期\]) )
> 
> RETURN
> 
> DIVIDE(TODAY()-A+1,B-A+1)

这样就实现了TODAY在本月、本季和本年的时间进度，如果你想用切片器任选一个日期，来查看该日期的时间进度，你可以将上述公式中的TODAY（）换成SELECTEDVALUE('日期表'\[日期\])就可以了。

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

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
