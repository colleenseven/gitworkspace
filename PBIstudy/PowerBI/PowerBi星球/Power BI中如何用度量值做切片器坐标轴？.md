---
ZK: Origin
notes: True
aliases: null
create_date: 2022-08-24T12:21:47 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: Power BI中如何用度量值做切片器/坐标轴？
source: https://mp.weixin.qq.com/s/EQlSPtwc7mishlCf6MK3TQ
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

DAX:: SWITCH, TRUE, IF, MAX,COUNTROWS,FILTER

---

经常有人问如何<mark style="background: #FF5582A6;">用度量值做切片器，或者如何放在图表的坐标轴上</mark>？基于度量值本身的特点以及可视化的制作逻辑，度量值不可能直接制作切片器，也不能用于图表的坐标轴，但并非不能实现同样的效果，本文通过一个例子来再现这个需求，并给出一个变通的解决思路。

下面这个可视化表格，是每个客户及其贡献利润的列表：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMs8LVkF6Jw9LMkbFBc3wbramUgHsibK6t9YefKGKp7A2s4atbDxlJu5yyfpSvf99KBI9HOVtBayJw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果要<mark style="background: #FF5582A6;">对客户做分类，定义利润贡献超过2000元的客户成为“高贡献客户”，1000元到2000元的成为“一般贡献客户”，而低于1000元的为“低贡献客户”</mark>。

对这个需求可以这样写个度量值：

> 客户类型 =
> 
> SWITCH(
> 
>     TRUE(),
> 
>     \[贡献利润\]>=2000,"高贡献客户",
> 
>     \[贡献利润\]>=1000,"一般贡献客户",
> 
>     "低贡献客户"
> 
> )

结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMs8LVkF6Jw9LMkbFBc3wbrlZ15o5nrT1Ps7tBtTydEa8EdcZ2u07uO3busMprVK9qK8CJrmSV9sw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个度量值的逻辑很简单，其结果会返回客户的三个类型。  

对于上面的列表，很多人想进一步设计，**把度量值放到切片器里筛选，点击哪个类型，列表中就只显示该类型的数据**，比如点击“高贡献客户”，表格中直接只显示相应的客户信息。  

这个需求看起来合情合理，不过<mark style="background: #FF5582A6;">度量值本身是个单一值，虽然看起来可以返回三种类型，但这是在不同的上下文环境下实现的，也是由于这个原因，度量值不允许做切片器，只有列字段才能做切片器</mark>，那么上述需求是不是无法实现呢？

当然不是，其实稍微变通一下，就可以很简单地实现。

先<mark style="background: #FF5582A6;">制作一个客户类型辅助表</mark>，如下。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMs8LVkF6Jw9LMkbFBc3wbryBG6ABz7YWw55PJnOYT4ic4ibT5TtazBNIwXWQCY5pWGRhCHaCSkwUBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

制作方式参考：[Power BI 辅助表制作方式汇总](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071809&idx=1&sn=9e8f4916082c32cc0291a2e4e565f1fd&chksm=8e0c4756b97bce4087ec53dfb6e5380e7cb0662e73fa070f831e4283095505a5aced233e59c8&scene=21#wechat_redirect)  

用<mark style="background: #FF5582A6;">辅助表的字段做切片器</mark>。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMs8LVkF6Jw9LMkbFBc3wbraqIQafbfw2fbh9JqhKzdLNHY3EGKsBkHAiafgN8mNt6Apbq7IxwMKQw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就实现了在切片器中显示出度量值返回的三个类型，下面只需要再写个度量值，将切片器与表格联动起来就可以了。

> 客户类型筛选 \=
> 
> IF(\[客户类型\]=MAX('客户类型'\[类型\]),1)

这个度量值的逻辑是，<mark style="background: #FF5582A6;">如果某个客户的类型等于切片器所选的类型，返回1。然后将这个度量值放到表格的筛选器中，只显示值为1的数据</mark>。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMs8LVkF6Jw9LMkbFBc3wbrlVOxhmCmNCnnpEN0Y85Z0fhMibGUibaIGtNBIKGOmhx9EGY98QoE8BQA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后切片器就可以与表格动态交互了：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMs8LVkF6Jw9LMkbFBc3wbrqRFSW5oJnFGqVshHpepucSgMY83K4JJPLnY0LVNTR76abwkPRImygQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样就实现了"度量值制作切片器"的效果。

另外，还有个常见的需求是，让度量值作为坐标轴，比如利用柱形图来展示每种客户类型有多少客户，如果直接把度量值放到坐标轴上，肯定也是做不到的，坐标轴同样必须是列字段。  

其实我们还是可以利用上面的思路，利用<mark style="background: #FF5582A6;">辅助表中的类型字段，放到坐标轴上</mark>，然后写个度量值，来计算每种类型的客户数量。

> 客户数量 按类型 = 
> 
> COUNTROWS(
> 
>     FILTER('客户',\[客户类型\]=MAX('客户类型'\[类型\]))
> 
> )

这个度量值的逻辑是，<mark style="background: #FF5582A6;">利用FILTER来筛选客户表中，属于当前上下文类型的列表，然后计算这个列表行数，得到当前类型的客户数量。</mark>

将这个度量值作为柱形图的值，就可以统计出每个类型的客户数量：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMs8LVkF6Jw9LMkbFBc3wbrzDkN1tB6IORRicDl9icU3icicd84JB56Twxiap1AbQUAxTJDm5SDOUjRC5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是"将度量值作为坐标轴"的效果。(更多关于客户类型的计算还可以参考这篇文章：[PowerBI业务分析：客户细分](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071357&idx=1&sn=e533d335e302b9ca5c76313dcac38852&chksm=8e0c416ab97bc87c1101fcbdb870356d9a400c68ba7c8ab6b91d4e6c54726b28cc358b6015fd&scene=21#wechat_redirect))

通过上面的例子，就变通实现了度量值作为切片器/坐标轴的效果，希望能为你的可视化设计打开一点思路。
