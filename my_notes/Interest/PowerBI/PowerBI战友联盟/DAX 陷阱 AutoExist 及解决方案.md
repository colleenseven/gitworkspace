---
create_date: 2022-04-19T13:17:58 (UTC +08:00)
tags: 
aliases: null
pagetitle: DAX 陷阱 AutoExist 及解决方案
source: https://mp.weixin.qq.com/s/lfA76Lxp8qpnqSYscXec5g
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

程序员不要吐槽本文的标题，我知道 AutoExist 不是陷阱也不是 BUG，这只是为了那些没有必要花精力理解这个不需要理解的概念的业务伙伴搜索标题时用的。

对于普通用户来说，你没有必要为了学习一个概念而学习一个概念。

这里讲述的这件事是纯 IT 的，因此，你需要做的是：知道这是什么事，然后收藏本文即可，无需理解也无需阅读完毕。

等你遇到这个问题的时候，在收藏中搜索 DAX 陷阱 即可回看本文。

至于：AutoExist 这个单词，你也一定不会记得的。

## 问题重述

来看一个例子，【场景 1】如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuHj0ssMtky54Q3SmzZdaCox5NToRMz2DcBQhUzEtQbwXs77h1CjDPEqdumJPh1yI7YqDqWQR7OQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中用的公式如下：

```
ProductCount = COUNTROWS( '产品' )ProductCount.All = CALCULATE( COUNTROWS( '产品' ) , ALL('产品'[产品子类别] ) )
```

很容易上图的内容，由于有 “产品类别” 的筛选，导致产品数是该两个大类别下的总数。注意：当前产品子类别没有被筛选。

记住这个数字：905，表示两个产品大类别下的产品数。

此时，选择一个产品子类别，来看看效果【场景 2】：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuHj0ssMtky54Q3SmzZdaCeuDK7qU5BAoHWiaK19h9tXeDtOgOiaaEXMVge4n6bFWk1mCWsbWDLpmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

产品子类别下的产品数：119，这是由于收到了产品子类别的筛选。

然而，对于清除了产品子类别筛选的计算，其结果是：461，而不是 905，这个结果非常诡异。

## 诡异之处

下面用清晰的逻辑来表述其中的诡异：

-   【场景 1】可知 “技术” 和 “家具” 下的产品数是 905；
    
-   【场景 2】看到清除了产品子类别的筛选后，“技术” 和 “家具” 下的产品数是 461；
    
-   【场景 1】与【场景 2】矛盾。
    

潜在结论：Power BI 出现了 BUG。

如果你学习了 DAX，你会这样想：

虽然 ALL (' 产品 '\[产品子类别\] ) 清除了产品子类别的筛选，但是它不会清除产品类别的筛选，因此，在【场景 2】中，清除了产品子类别的筛选，但受到与【场景 1】中相同的产品类别的筛选，因此，结果应该是：905，而实际结果是 461，这很诡异，像是一个 BUG。

如果不是 BUG 的话，那么一定出现了更复杂的情况。

## 一定会遇到的陷阱：AutoExist

业务的小伙伴不必理解这里说的东西，后文会给出解决方案。

这里的确不是 BUG，而是 Power BI 的 DAX 引擎就是这么设计的，这里触发了 DAX 在计算时候的一个机制导致了这种效果。这个机制叫：AutoExist。

若满足以下条件则会触发该机制：

若在某个表上存在两列或以上的筛选，该筛选将参与 SUMMARIZECOLUMNS 运算，则会触发 AutoExist 机制，该机制将某个表上存在两列或以上的筛选先合并成一个筛选，再参加计算。

这里要满足两个条件：

-   同一个表的两个列或以上的筛选。如：本例中的产品子类别以及产品类别的两个列。
    
-   要参与 SUMMARIZECOLUMNS 运算。如：在 Power BI 中所有图表都是由 SUMMARIZECOLUMNS 返回的运算结果。
    

不难看出：

在 Power BI 中使用任何图表都会自然的触发条件 2，而用户的确常常会做切片器，而且来自同一个表的不同的列，那么，也很容易触发条件 1，这样一来，这个叫

AutoExist 的机制是很容易被触发的。

因此，Power BI 用户，尤其是编写了 DAX 的公式，大概率会遇到这个问题的。

## 为什么要有 AutoExist

由于本文一上来讲了一个问题，导致大家可能对 AutoExist 有个先入为主的不好印象，其实，AutoExist 是一个在不知不觉中帮助我们的重要机制。Power BI 要解决的重要问题就是：

如何在一个巨量的数据空间中，迅速缩减到图表所需要的一个数据子集，通过筛选实现这个目的，而一个表上的多个筛选，如果在计算时分别对待，则会触发笛卡尔积的排列组合运算，导致性能问题，而 AutoExist 机制正好将不可能出现的排列组合给预先剔除掉，确保没有笛卡尔积的问题。

而幸运的是，在绝大多数情况，这种机制都工作良好，用户是不会发觉有什么特别的东西在后台运作，用户只是感觉 Power BI 筛选数据好快好快。

## 案例解析

已经知道了 AutoExist 的运作机理以及它的意义，而且绝大多数都不会出问题，那么，本案例中的问题是怎么被触发或者说不幸的成为一个问题了呢？

在出问题的【场景 2】中，其筛选是这样的：

表列：产品子类别 IN {"复印机"}

表列：产品类别 IN {"技术","家具"}

由于表列：产品子类别和表列：产品类别都来自同一个表：产品表，则它们在进入计算前，会被合并，如下：

由于在产品表中，产品子类表的 “复印机” 是与产品类别的 “技术” 对应的，而没有与产品类别的 “家具” 对应的可能，因此，这个筛选得以合并为：

(产品子类别，产品类别) IN { ( "复印机" , "技术" ) }

也就是说：“家具” 消失了。

因此，可以推断案例中【场景 2】的结果 461 应该是：产品类别 “技术” 下的所有产品，而不再包括产品类别 “家具” 下的产品。验证如下：

果然如此。

通过观察 DAX 公式，以及触发了 AutoExist 产生的问题，可以总结到：如果在公式中有 ALL 掉某表一部分列且报表中有来自该表的多个列的筛选时则可能触发此问题。

## 解决方案

由于触发 AutoExist 需要两个条件，其中 SUMMARIZECOLUMNS 运算是不可避免的，在 Power BI 中图表都默认使用了这个计算，那方案只有是不让它来自一个表的多列。那么，在触发了 AutoExist 陷阱的时候，将来自同一个表的多列分别构造独立的维度即可。如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuHj0ssMtky54Q3SmzZdaC0wUlzNtpdeGCclceb5Mzo4vuNRV0fYB6ibZKHsyS9YLIgOxJ4iclCqIQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

此时，来看下效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOuHj0ssMtky54Q3SmzZdaCsKYbqHMnq6z5yib7qdqqJ7CrDmasC75MsWrQxll095YY38zMkdVLpibQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

此时，看到了正确的结果 905 个产品。

## 总结

AutoExist 是内置于 DAX 底层运算中用于提升性能的技术特性，它在绝大多数时候都扮演了积极且重要的角色，但有时可能会导致副作用，这种可能导致副作用的诡异现象的触发条件常常如下：

-   度量值的公式中有修改（如：清除，常常使用 ALL）某表一部分列筛选
    
-   报表中有来自该表的多个列的筛选
    

则 AutoExist 特性在后台自动运转时可能导致诡异的计算结果，称此为：AutoExist 问题陷阱。

需要注意的是：AutoExist 是故意这么设计的，它既不是 DAX 的缺陷，也不是 DAX 的 BUG，只是由于对 DAX 运行原理不够了解而踏入的一个陷阱。

更要注意的是：业务人员永远不需要去也不应该去了解该特性的技术细节，正如本文的绝大部分文字都可以不必阅读。只需要记忆：

-   DAX 有个陷阱叫：Auto 啥的来着。
    
-   当一个表有两列分别作为切片器时又写了一个 DAX 公式里 ALL 掉了其中一列。
    
-   数字就会不对。
    
-   解决方法是：把那列单独做个表出来即可。
    

时间来到 2022 年，Power BI 的学习方式已经不是几年前，一起高喊 DAX 牛逼的日子，而是精细化的拆解出一套业务人员与技术人员的有效区隔，业务人员应该将注意力集中在业务本身，以及如果使用 DAX 来表达业务问题本身。业务人员只需要知道：

-   怎么做是一个正确而安全的习惯
    
-   如何识别潜在的问题
    
-   当出现问题了如何快速修复
    
-   继续关注业务本身
    

这是我们将持续为业务分析师带来的价值。毫无疑问，这些都会囊括在《BI 真经》的内容中。

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNhia5Pc4XC1Um7IYgQhGEoEC1yK05ibUFoPBYpcoAMvibuZh2BZaibMzULeDwNfSeQ0KHRcDUdX3FzVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**Power BI 终极系列课程《BI真经》**

[

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/09hv4Xua0LNBM1lxlQYHJBicic4CvPoRGLqHgdTZOr8goNRh0asDXA48mRDzc9zxW4UMQiayHwgDmx7mlt4cQxtjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
