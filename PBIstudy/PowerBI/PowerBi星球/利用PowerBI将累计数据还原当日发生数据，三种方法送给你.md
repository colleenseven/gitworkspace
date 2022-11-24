---
ZK: Origin
create_date: 2021-11-16T12:54:42 (UTC +08:00)
tags: 
aliases: null
pagetitle: 利用PowerBI将累计数据还原当日发生数据，三种方法送给你
source: https://mp.weixin.qq.com/s/qR8dKCRUQmjgkj2tFf1Ydg
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

你也许也遇到这样的情况，数据中的每日记录是历史累计数，而需要分析的是当日发生数据，这就需要将累计的数据还原为当日数据，在PowerBI中，有多种方式可以实现这种计算。

模拟示例数据如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO7wYygGHNvXUJxibw3WBHLX6jsic8kIbvrfBqpJB9wDlBTBjjtetyBiaEpxH21WVZ15rusJ8HnINnsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个数据中记录了每个用户的每日历史累计数据，下面就通过这个示例介绍如何用M以及DAX来计算出当日数据，并帮你理解这些方法的异同之处。

**Power Query法**

在PowerQuery的界面功能中，无法直接实现，这种情况下我们就需要用M来计算。  

将数据导入到PowerQuery编辑器中，添加自定义列：

```
List.Sum(
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO7wYygGHNvXUJxibw3WBHLXOsskoLd0yMUNqDyxrbNNxAibeYnpbkr64ibwM6DaCrXxhSpDZ0Qic4QnA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个M公式的难点主要是如何计算上一日的累计数，它是利用Table.SelectRows来筛选行，筛选的条件就是：

(x)=>x\[日期\]=Date.AddDays(\[日期\],-1) and  x\[用户\]=\[用户\] 

也就是日期是当前日期的上一日，并且用户等于当前用户的行，获取该行的累计数据，就是上一日该客户的数据，然后用本行累计数据减去上一日的累计数据，便是本客户的当日发生数。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO7wYygGHNvXUJxibw3WBHLXzojgEb4MtqficBQ6o4NibywgewfxoRGP3hDMeeOfmeM2HYibfiaO8eMWqg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于这个M公式，你需要有一点语法基础才能看懂，如果暂时看不懂也没有关系，记住这种套路，需要的时候可直接套用。

上面是用M实现的，用DAX当然也可以实现，下面就分别介绍计算列和度量值实现的方式。

**DAX-计算列法**

计算列的写法如下：  

关键是第8行的表达式，筛选逻辑与上面的M完全一致，只不过这是DAX的表达方式，也是根据当前行的日期和用户，找出上一日相同客户的累计数据，最终的结果与PQ也是一样的。

**DAX-度量值法**

将数据表中的日期和用户作为上下文，度量值就可以这样写：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO7wYygGHNvXUJxibw3WBHLXEicWIWdtOw4e1JotEUwoEu87ib2TaNfgIZjzOaUYD1aZ7pRB3ia8cmeOQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其结果也是一样的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO7wYygGHNvXUJxibw3WBHLXPQm0fTjfeA1zdIfZTJZVae7FjnEz6uSxY5HbpY4OxUJuTlXM4SSic2A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

仔细观察度量值和计算列写法的区别，其中最关键的一点是，在度量值中，并不需要在筛选表达式中指定，用户与当前行的用户一致，因为度量值会自动接受当前外部用户上下文的筛选。

如果在模型中建立日期表，构建数据模型，其实还可以用时间智能函数来实现这种需求，度量值写法更加简单。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO7wYygGHNvXUJxibw3WBHLX3EeicX45Lb0vibBktyNcoSdd4iciapx4j35LISBMic8ZHqPftqJAt8eT60Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

直接使用PREVIOUSDAY筛选上一日，计算上一日的累计数据，然后相减得到本日的发生额。

其实度量值可以直接得到每日发生额，无需在PowerQuery中添加自定义列，也无需在模型中添加计算列，非必要时也不建议在数据中添加列，度量值才是推荐的做法。

___

上面几种方法，整体的计算逻辑是一样的，都是先筛选出上一日同一客户的累计数，然后通过本日的累计减去上日累计数得到。只不过筛选的方式略有差异，除了M和DAX函数和语法本身的差异，关键是上下文的影响：

-   M的上下文是表的当前行，不能自动筛选，需要显式的M表达式进行筛选；  
    
-   计算列的上下文也是当前行，行上下文不能自动筛选，需要需要显式的DAX表达式进行转换；  
    
-   度量值的上下文是各种外部筛选器，可以自动产生筛选作用，对于不需要转换直接应用的筛选器，无需在DAX内部显式表达。
    

以上就是将累计数据还原为当日数据的几种方法，关键是通过这个简单的计算掌握各种方法的筛选逻辑。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
