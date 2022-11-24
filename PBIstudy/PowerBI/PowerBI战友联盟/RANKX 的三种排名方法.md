---
create_date: 2022-06-07T13:09:54 (UTC +08:00)
tags: 
aliases: null
pagetitle: RANKX 的三种排名方法
source: https://mp.weixin.qq.com/s/W16UpNU-gPTffhmN344YMg
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月07日 20:00 直播

PowerBI

视频号

对于排名，是一个老生常谈的问题，有小伙伴问：

如何实现完全顺序排名？

先来看看效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMWRPibiceXYYzWn4ribT3wmjOED5zr8nOnJG0mcGHYbXFFx966IjUsIa6GPSTNZfbgRA0oO5r76LFCg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里分别列出了针对 Item 的每个值以及对应的排名。

-   Dense 方法：RANKX 原生支持，称为紧密排名。
    
-   Skip 方法：RANKX 原生支持，称为稀疏排名。
    
-   Order 方法：自定义实现，RANKX 无原生支持，称为自定义顺序排名。
    

## Dense 方法

编写度量值如下：

```
Item.Rank.Dense = RANKX( ALLSELECTED( Data[Item] ) , [Item.Value] , , , Dense )
```

注意，多个逗号之间不写内容属于忽略的参数。可以参考此前关于 RANKX 的文章。

## Skip 方法

编写度量值如下：

```
Item.Rank.Skip = RANKX( ALLSELECTED( Data[Item] ) , [Item.Value] , , , Skip )
```

注意，多个逗号之间不写内容属于忽略的参数。可以参考此前关于 RANKX 的文章。

## Order 方法

编写度量值如下：

```
Item.Rank.Order = VAR vItemIndex = RANKX( ALLSELECTED( Data[Item] ) , [Item] , SELECTEDVALUE( Data[Item] ) )RETURN    RANKX( ALLSELECTED( Data[Item] ) ,         [Item.Value] +        RANKX( ALLSELECTED( Data[Item] ) , [Item] ) / 100 ,         [Item.Value] + vItemIndex / 100     )
```

这里的构思技巧在于：

第 5 行，计算每个 Item 的值。

第 6 行，计算每个 Item 的自身的索引并作为一个小值加到值的身上。

第 7 行，用当前元素的值和索引量在排序表中卡位实现计算排名。

在这个方法下，每个元素都不会出现重复的值，因此实现了顺序排名。

## 总结

RANKX 非常简单，只要你明白了它的本质原理即可。

更多参考：[PowerBI DAX RANKX 详解](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650784752&idx=1&sn=d66d858f845d1340bd436fe531684e4b&chksm=f18cc3e1c6fb4af720eab2e27912a3ba60829263996ac454ede8cff08f6a6396b279b6f466c1&scene=21#wechat_redirect)  

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月07日 20:00 直播

PowerBI

视频号

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

**Power BI 终极系列课程《BI真经》**

[

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
