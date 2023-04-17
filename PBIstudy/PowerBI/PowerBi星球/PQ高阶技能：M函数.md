---
create_date: 2017-12-29T20:51:50 (UTC +08:00)
tags: wx/pbi/PQ数据处理 
aliases:
pagetitle: PQ高阶技能：M函数
source: https://mp.weixin.qq.com/s/UHVNcTrqcQuhEn373G70XA
author: 采悟
status: 已完成 
category: 精读文章 
notes: false
ZK: Origin
uid:
---

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG24ribzcPPPzWnq5zBibndI78xOJF0WPaGoQRiaoakHiaKgojVviaURNzSW7Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

前面我们学习PQ的时候都是用鼠标操作，虽然通过这些操作能完成大部分的数据处理，但是毕竟还有些复杂的工作是处理不了的，如果想彻底驾驭PQ，必须得掌握点高级玩法。就像学习Excel一样，做个表格我们只要会简单的操作就可以了，但要想学好Excel，必须会点公式、VBA是一样的道理，PQ的高级技能也是需要写公式函数的，在PQ中用的函数称之为M函数。

___

在之前的PQ操作中，其实M函数无处不在，比如做数据清洗的每一个步骤，背后都有M函数的影子。打开高级编辑器，可以看到所有这些步骤的M语言。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMowD7iaZ9YHlvxMwgl5k3EQ3GT17xAqVrfK2LlHiaXiad6aKjsDkzwfsW59sFtvOQjvSavYU9pqBoqQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果我们不进行鼠标操作，直接在编辑器中编写这些语言，也是可以得到最终的结果的，有了M函数，PQ的数据处理具有很强的可读性和可移植性。

**01 | 为什么要学习M函数**

-   有些复杂的操作必须借助M函数
    
-   M函数更加灵活，简洁高效
    

**02 | M函数基本规范**

-   ==M函数对大小写敏感，每一个字母必须按函数规范书写，第一个字母都是大写==
    
-   ==表被称为Table，每行的内容是一个Record，每列的内容是一个List == 
    
-   ==行标用大括号{ }，比如取第一行的内容：=表{0}   //PQ的第一行从0开始==
    
-   ==列标用中括号\[ \]，比如取自定义列的内容：=表\[自定义\]==
    
-   ==取第一行自定义列的内容：=表{0}\[自定义\]==
    

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMowD7iaZ9YHlvxMwgl5k3EQKqPfQP8tpBWnZN6Jz8Zwj9Orzh72Q7P46Ek9XaBAr058M4h8AQFIfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**03 | 常用的M函数**

-   聚合函数：  
    

> 求和：List.Sum()
> 
> 求最小值：List.Min()
> 
> 求最大值：List.Max()
> 
> 求平均值：List.Average()

-   文本函数：  
    

> 求文本长度：Text.Length()
> 
> 去文本空格：Text.Trim()
> 
> 取前n个字符：Text.Start(文本,n)
> 
> 取后n个字符：Text.End(文本,n)

-   提取数据函数：
    

>   从Excel表中提取数据：Excel.Workbook()
> 
> 从Csv/Txt中提取数据：Csv.Document()

-   条件函数：
    

>   if  else then （相当于Excel中的IF)

**04 | 从哪里查找M函数**

新建一个空查询，在公式标记栏中输入#shared，就把所有的M函数显示出来了，点击某个函数，最下方便出现该函数的注释：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMowD7iaZ9YHlvxMwgl5k3EQiafYppqfw9uBePqDnR8Z0lkMClB7YROLSSMTVHDhukMkpPCgHwxGKjg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**05 | 学习建议**

虽然M函数很强大，但是不建议一头扎进去学习她，毕竟对于一个之前没有接触过编程的人来说，学习成本还是挺高的，并且大部分函数并不常用。

**我的建议是先能够读懂M语言，并把常用的函数，比如文本函数、字符串函数、日期函数等浏览一遍，知道大概都有什么函数，分别是哪些功能，然后在数据处理过程中碰到鼠标操作难以完成的问题，能想到有哪个M函数可以利用，直接查找和并根据注释使用、或者会修改相应的M函数即可。**

如果熟练使用鼠标操作功能，又能灵活运用M函数，你将在数据处理的路上一骑绝尘、所向披靡。在大数据已经进入日常工作和生活的今天，拥有Power Query这个利器, 我们就能用最少的时间来处理数据，留下更多的时间去分析数据，去发现数据背后的规律，这才是我们学习PQ、学习PowerBI的最终目标。

**Power Query学习系列：**

[体验Power Query](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067120&idx=1&sn=4188548c00910c7e9fd1cb5c2d5f8880&chksm=8e0c71e7b97bf8f135ea0bc07fff83152b9cf0ecc24b504eff1f999d92b65b58d0a4939c2c84&scene=21#wechat_redirect)

[数据获取](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067131&idx=1&sn=cac2f0f5b79169cbba61bf207bee1532&chksm=8e0c71ecb97bf8fa211533583fcf92f374a96d3eba85c1cffabbac3639d40335fbd188761f7d&scene=21#wechat_redirect)

[数据清洗](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067158&idx=1&sn=4ad955112df2f40a93b684ed9147f26e&chksm=8e0c7181b97bf89777ae3d9de929867745edcbbfe1f2b396761c0cec716b86ee31e439279add&scene=21#wechat_redirect)

[数据丰富](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067174&idx=1&sn=e60839949f8117c892d4f1c1f8f74f12&chksm=8e0c71b1b97bf8a7b20c9c48d7702a2d7b06721fd054605024b2378393f06f624f0d1a4d1e6b&scene=21#wechat_redirect)

