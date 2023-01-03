---
create_date: 2023-01-03T23:40:54 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI如何统计文本中字符出现的次数？
source: https://mp.weixin.qq.com/s/N3EibihBexMg5Mz8HGyIlQ
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

统计一串文本中某个字符出现的次数是很常见的需求，也有很多星友提问过，这篇文就来整理一下如何用PowerBI来进行这种计算。

以下面这个数据为例，

**![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1No79s8hRicqPybaVJDbpOtia6nrQuBLUJy9AXicfCn22tiajFhaOqx3Ckfs5A9dscgeXEybrY3XxJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)**

**如何计算出每一行的文本中，斜杠字符"/"有多少个？**

下面通过M和DAX两种函数来看看如何实现这种需求。

**方法一：利用M直接统计字符法**

在PowerQuery编辑器中添加自定义列：

> List.Count(
> 
>     List.Select(
> 
>         Text.ToList(\[文本\]),
> 
>         each \_="/"
> 
>     )
> 
> )

这个表达式的逻辑是，先通过  Text.ToList将这一串文本拆分成每个字符的列表，然后通过List.Select筛选其中为"/"字符，最后通过List.Count统计字符的个数。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPKdViaQCjjHzmjL4AQKBXxNAttIgNpjcZrOJK2gYv41CPIsoyBDuGYVs5rEQ1xV9X1VMht4x1QsaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**方法二：替换后计算长度差异法**

这个方法的思路是将需要统计的字符移除或者替换为空，然后统计替换前后字符长度的差异就可以实现了。  

M函数可以这样写，添加自定义列：

> Text.Length(\[文本\])
> 
> \-
> 
> Text.Length(Text.Remove(\[文本\],"/"))

这个方法比较简单，并且不仅是M函数，用DAX也可以用同样的思路计算。

**方法三：利用父子函数巧妙实现**

使用DAX，除了上面的方法，其实还可以结合父子函数的逻辑巧妙地统计出来。  

在DAX中新建列，将要统计的字符，这里就是"/"，利用SUBSTITUTE函数，替换成 "|" ,替换后的结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1No79s8hRicqPybaVJDbpOyzykzrwlavIK31xlhDDMzBC5mXj8SPic0ibGyr0b3RxvEYLZBQpuyibFg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

你也许不是很理解为什么要替换成这样，但是如果熟悉DAX中的父子函数，应该能看出来，替换成"|"后的效果类似于父子层级结构，我们可以利用父子函数中的PATHLENGTH，来统计层级深度。

因为带有1个"|"，代表有2个层级，2个"|"，代表有3个层级，以此类推，层级数减去1就是"|"的个数，也就是我们要查找字符的个数，结果如下：  

[参考:利用这个经典应用场景，学习PowerBI父子函数的用法](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078287&idx=1&sn=5da26f894eb0cbf484a7b2b2df2407c8&chksm=8e13ac18b964250e383d551ef2dacb46cc33f5da2cfb7d2b5ffb522c7c2a88d14ce289ec6104&scene=21#wechat_redirect)  

其实熟悉了这个原理，我们可以一次性就把它计算出来：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1No79s8hRicqPybaVJDbpO6WfHwvibtfm6IegK7qYyNZhyVf5OZx4f6TlkcWWEgBGxtNOXkgw68Tg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过上面几种方式，利用不同的函数、不同的算法，实现了同样的需求，这些技巧你学会了吗？

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
