---
create_date: 2022-11-16T11:28:44 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerBI 四象限通用分析模式系列之一
source: https://mp.weixin.qq.com/s/3qxcsrCLTibsri2-U6Epzw
author: Toby
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

> BI 佐罗
> 
> Power BI 作为自助商务智能分析的代表工具，已经将分析本身推进到了业务案例时代。众多作品和案例已经在实际业务中纷纷涌现，这包括了常见的所有行业（零售，快消，医疗，互联网，教育，咨询，金融等），职能（财务，HR，运营，销售，决策等）。我们也会邀请相关伙伴分享真实案例以及模式抽象。
> 
> 很多小伙伴问，如何可以从业务的角度给出通用的分析模式，这次我们邀请顶级作品案例作者 Toby 为大家带来四象限分析解读系列的干货内容，供大家从业务的视角来感受四象限分析模式可能带来的分析收益。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwBsvDw2T2zGaJ8mVoDR1yHohBdnP6K41ibeYJsXvC79KHMBGkL4NCCibzA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在 Toboyoo 分析看板中，有一个专门的模块，通过 80/20 原理，建立起 “四象限分析” 模型。该模型从【组合象限】、【80/20 数字】和【年度变化】3 个主要子页面进行分析展示。如下所示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwB16oAtx84cl7euPG6vZbib69SXEgib44vQrvWQUvPOdcic135WkD9KrRAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

该模型具有通用性，可复用。为让大家更好地理解该模型并应用于工作中，接下来我们将分阶段对该模型进行解析。该系列会有多篇介绍，本文为第一篇，讲解基础概念。

## 什么是 80/20

大家熟知的八二法则指出，仅约 20% 的因素，可影响 80% 的結果。在一个公司内，绝大部分的价值来至于少量的客户 / 产品，换言之，大部分的客户 / 产品只贡献少部分的价值。因此，我们可以将业务划分为 80/20 客户和 80/20 产品：

-   80 指的是少数关键的客户 / 产品，他们带来了高达 80% 收入。
    
-   20 指的是大部分普通客户 / 产品，他们只提供 20% 的收入。
    

在实际应用中，我们可根据需要，把该法则用于其他分析对象或指标。在 Toboyoo 的案例中，我以门店（Store）和产品（SKU）作为对象、毛利润额（Gross Margin）作为指标进行分析。（选择利润额作为指标，是为了从投资方的角度来看公司的运营管理，毕竟经营一个公司的最终目标还是要看最后属于自己的钱到底有多少）

根据划分后的结果，可看到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwBs0bR9pLaXgzOueSQCOkj0dFxsKz9LkpSl2AXp9uHHTgVIicEmvCv47g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

-   全球 305 家门店，其中 177 家门店贡献了约 80% 的毛利润即 $ 1,236,465,627；剩余 128 家门店贡献了剩余 20% 的毛利润即 $ 301,552,377
    
-   全部 1244 个 SKU，其中 369 个 SKU 贡献了约 80% 的毛利润即 $1.237,896,876；剩余 875 个 SKU 贡献了剩余 20% 的毛利润即 $ 300,121,128
    

到此，我们可以先思考：

-   如果将 20 门店（128 家）的投入追加投资在 80 门店（177 家），对公司的利润会有什么改变？
    
-   如果将 20 SKU（875 个）的投入追加投资在 80 SKU（369 个），对公司的利润会有什么改变？
    

## 如何计算 80/20 并组合四象限

80/20 的计算过程如下：

-   将过去一定时间内（通常选择 12 个月）每个门店 / SKU 所得的利润额汇总
    
-   将利润额按门店 / SKU 由高到低进行排序
    
-   计算每个门店 / SKU 的利润额在总利润额中的占比
    
-   从利润额最高门店 / SKU 开始，向下累积门店 / SKU 的利润额在总利润额中的占比直至 80% 左右，这些累积的客户或者 SKU 就是代表 80% 利润额的客户或者 SKU
    

通过对 80/20 进行组合，可形成以下四象限：

-   象限一：80 门店销售你的 80 SKU（占 64% 的利润额）
    
-   象限二：80 门店销售你的 20 SKU（占 16% 的利润额）
    
-   象限三：20 门店销售你的 80 SKU（占 16% 的利润额）
    
-   象限四：20 门店销售你的 20 SKU（占 4% 的利润额）
    

于是形成：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwBbNVwYdjhEuWvBevv4Q8eibjXic2Dnj7IQ24yXcuaDABQDuZEaOSS8MYw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

完成四象限后，你会发现你的业务主要是由那些顶级门店 / SKU 驱动的。也能发现哪些门店 / SKU，几乎没有给收入带来什么价值，反而会降低利润。

## 简要分析

对比 80/20 门店，可思考以下问题（包括但不局限）：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwBicFkt6x4bTcfib3u1fMTcStpAWrkdrzWC7eCEbWmAJnCDQvvicTYEfGkQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

-   为什么 80 门店的平均单价高于 20 门店？
    
-   为什么 80 门店的平均毛利润率高于 20 门店？
    
-   是由于定价问题、SKU 组合问题造成还是折扣问题造成的？和地域分布是否有关系？和渠道是否有关？和品牌是否有关？
    
-   门店下一步需要做什么？
    
-   现阶段有没有什么可能需要采取的临时措施？
    

对比 80/20 的 SKU，可思考一下问题（包括但不局限）：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwBDgm0dxKJEJYicyacGDyNZnlbCzEQStvoLNwgmddViapg7AW77AicvuqMw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

-   为什么 20 SKU 的平均单价远低于 80 SKU？
    
-   为什么 20 SKU 的利润率远低于 80 SKU?
    
-   与 SKU 类别和 / 或生产商是否有关？和地域是否有关？和渠道是否有关？和 SKU 组合是否相关？和品牌是否有关？下一步分析是什么？
    
-   现阶段要不要采取什么临时措施？
    

对于四象限，可思考一下问题（包括但不局限）：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwBMd30vH4WYy6fJibWicc424LicUttk1o0v02GHibr6p77mcjsevLzGETxOg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

-   利润率分析：平均利润率 49.6%，为何第二、第四象限利润率明显低于平均数，特别是第 4 象限？这种情况按照年、SKU 类别和子类别，渠道、地域和品牌是否仍然存在？有没有负利润率的 SKU？
    
-   单价分析：为什么 80 SKU 单价第一象限高于第三象限；20 SKU 第二象限高于第四象限？
    
-   第一象限的门店和 SKU 有什么特点？
    
-   有没有只在第四象限的门店 / SKU？
    
-   有没有 20 门店具有 80 门店的潜力？
    
-   ...
    

## 总结

> BI 佐罗
> 
> 四象限分析是将业务按照不同维度划分后展开对比进而引起启发式思考的通用模式，在本案例中已经给出了该模式的概念，解释，计算逻辑，可以启发思考的业务问题。
> 
> 大家完全可以在自己的业务中借助这套思路来构建符合自己所在领域或职能的四象限分析。
> 
> 感谢 Toby 的解读，也期待本系列的后续文章。
> 
> 如果你在工作中有积累的干货思想，也欢迎与我们联系，共同探讨。

你发现本文中的一个问题了吗？你有没有疑惑？我们将邀请 Toby 在直播间与我们一起分享探讨。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/MfTd6rd9CyvNRMW8I9cvI1CK5gKiaYqg2veTn9t9dAe1GxYic7pAvgvRIKNFickConFyX8AvW2reAq8GchJI6aBpA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

【BI佐罗&嘉宾论数】直播间  
免费参加案例讨论直播《Toboyoo》课程专属专题  

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

BI佐罗&嘉宾论数：四象限通用分析模式

视频号

该作品案例可直接参考：

excel120.com/go/case/toboyoo

建议在PC端欣赏整个案例  

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LMAjDwBTzXmuvpgoTPDeWwB2JLtcFgEvRZhqdcHtmgQvv54NicToA86zTdoD9ouruTsdBTbKEQIlPg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)  
最强大的 Power BI 案例体验学习中心

excel120.com/pro  
（从免费到企业级顶级专家PowerBI智库）  

**Power BI 终极系列课程《BI真经》**

[

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

**BI佐罗严选推荐：[必学书籍](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796095&idx=1&sn=16377fdcb6da7fc03a68b6e92d840a23&chksm=f18cf02ec6fb7938daa266bcf8ef723ddf54abe6050126f77391e0d6d95b204eaf825b2831fb&scene=21#wechat_redirect) [精英眼镜](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796099&idx=1&sn=0e98a588f53c58b2ed3d890737b390dc&chksm=f18cf052c6fb7944fabc3564b8d5abc667348888a5384936c72b2710765d1ea8d22e6f6d5d8d&scene=21#wechat_redirect) [线下沙龙](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650796587&idx=1&sn=9cfcda5211b6bb82bbe4dd468079bd01&chksm=f18cf23ac6fb7b2c7d50a34ad68a775e464e6269d9c83e675ab4d8027c667d3d4dcf09b1578d&scene=21#wechat_redirect)**

扫码与精英一起讨论 Power BI，验证码：data2022

点击“阅读原文”  
立刻拥有此案例

**↙**
