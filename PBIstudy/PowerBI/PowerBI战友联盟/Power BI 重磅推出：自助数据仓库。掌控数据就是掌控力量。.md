---
create_date: 2022-06-01T13:10:53 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 重磅推出：自助数据仓库。掌控数据就是掌控力量。
source: https://mp.weixin.qq.com/s/BdP7FYvKbhrXNNO19zS4_Q
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

> 数字化未来已至，掌控数据就是掌控力量。

## 发生了什么  

业务用户严重依赖由信息技术团队 (IT) 构建的集中管理的数据源，但 IT 部门可能需要数月时间才能对给定数据源进行更改。作为回怼，用户经常假装求助于使用 Access 数据库、本地文件、SharePoint 网站和电子表格构建自己的数据集市，从而导致缺乏治理和适当的监督，以确保此类数据源得到支持并具有合理的性能。

数据集市有助于弥合业务用户和 IT 之间的差距。Datamarts 是自助式分析解决方案，使用户能够存储和探索加载在完全托管数据库中的数据。数据集市提供了一种简单且可选的无代码体验，可以从不同数据源提取数据，使用 Power Query 提取转换和加载 (ETL) 数据，然后将其加载到完全托管且无需调整或优化的 Azure SQL 数据库中。

将数据加载到数据集市后，您还可以为商业智能和分析定义关系和策略。数据集市自动生成数据集或语义模型，可用于创建 Power BI 报表和仪表板。您还可以使用 T-SQL 连接或使用 SQL 查询数据集市。

如图所示：

很多小伙伴会问：什么是数据集市？和数据仓库有什么区别？

其实是这样的：数据仓库，是把企业所有数据都搞到一起存好，一般只能由 IT 搞的。而数据集市，是一个低调的称呼。这样比较给面子，数据集市大到一定程度，和数据仓库本质一样。只不过你这么说的话，IT 肯定不喜欢的。所以，要低调的，这样就是在数据仓库的基础上，架设一个由业务人可以控制的数据集市。

那数据集市可以放多少数据呢？可以放多达 TB 级别。

那数据集市有什么好处呢？

-   业务人员无需求助 IT 管理员即可自主轻松构建可支持多达 TB 级别的数据库并进行分析。
    
-   整合海量数据不需要写代码，使用图形化界面利用 Power Query 拖拽生成即可。
    
-   支持直接构建统一的业务逻辑层，为所有人在其上工作提供了 “数据加逻辑”。
    

也就是说：

无需 IT 帮助即可零代码（或 PQ+DAX）构建自带业务逻辑的可支撑到 TB 级的数据中心。

虽然，这个描述比较夸张，但只有夸张才能强调本质。

你们知道吗：当年 Power BI 推出了 Power BI Premium Per User 且业务部门可以自行购买，微软立马收到了大量 IT 投诉，因为业务可以绕过 IT，自己购买和开通 Power BI，也就是开通数字化超级能力。微软妥协了，在这个功能上加了一个开关，IT 可以关闭这个开关，让业务需要购买 Power BI 的时候必须经过 IT。IT 的理由是：这样才能统一管理。这个理由当然合理。当我们只是指出这个背后在职场中的另一种可能而已。

当然，本处的数据集市只是提供了这种能力：无需 IT 帮助即可零代码构建自带业务逻辑的大数据中心。

在实操中，你会收到各种理由，告诉你做不了的。

所以，和 IT 搞好关系是王道。

当然，在拥有智慧的组织里，实际情况正好是相反的：

-   IT 嫌业务太麻烦了，最好业务人员可以自己搞定，IT 特别希望业务可以自己搞这些，那么，IT 就可以腾出来精力去做更技术的事情了。这对 IT 来说，是重大利好，IT 控制数据源头，而如何使用数据就交给业务用户即可。
    
-   业务嫌 IT 太慢了，最好可以接通数据，自己部门的 Power BI 高手可以搞定一切了。
    

没有错，在不良的合作关系中，这个技术发挥不出来；但在良好的合作关系中，不管是 IT 还是业务都将得到崭新的竞争力。至于你的实际环境是哪种，可以自己对照。

## 数据集市的特性

Power BI 推出的数据集市具有以下重大特性：

-   纯云端操作，无需任何软件。
    
-   零代码体验，现在无需以后也无需学习 SQL 就可以搞定一切。
    
-   性能自动优化。无需数据库专家，性能自定优化。
    
-   内置图形化编辑器，支持 SQL 查询以及混合分析。
    
-   支持程序员用 SQL 客户端去连它。
    
-   与 Power BI 和 Office 原生集成。
    

## 谁可以使用

如果你的企业已经是 Power BI Premium 租户或者你是 Power BI Premium Per User 客户，那以上一切已经为你准备好了。

顺便提下：

-   第一，企业 Power BI Premium 是个人不需要了解的。
    
-   第二，如果企业没有，那么个人购买 Power BI Premium Per User 费用大概：1500 RMB / 人年。
    

如果你在大型企业或外企，可能你已经是满足一了。如果你是个人或者在中小企业，那你就知道第二条将告诉你这是怎样的性价比。

## 什么场景用

那么什么时候来用数据集市呢？

数据集市，用于解决没有 IT 帮助你的情况下，自己要搞定一切时又不会写代码时的工作压力。

例如，如果您从事会计或金融工作，您可以构建自己的数据模型和集合，然后您可以使用它们通过 T-SQL 和可视化查询体验自助服务业务问题和答案。此外，您仍然可以将这些数据集合用于更传统的 Power BI 报告体验。数据集市推荐给需要面向领域、去中心化数据所有权和架构的客户，例如需要将数据作为产品或自助数据平台的用户。

进一步来说，数据集市可以用来支撑以下场景：

-   部门级数据中心。低调了。将小到中等的数据量（大约 100 GB）集中在一个自助式完全托管的 SQL 数据库中。数据集市使您能够为自助服务部门下游报告需求（例如 Excel、Power BI 报告等）指定单个商店，从而减少自助服务解决方案中的基础架构。
    
-   一个大型 Power BI 分析。内置构建数据模型，支持编写 DAX 度量值等构建一个大型的 Power BI 方案。
    
-   完全自助控制的业务模型。让 Power BI 用户可以在不依赖 IT 或其他工具的前提下，构建业务逻辑，使用可视化的界面，而一切都存储在云端数据库，比放在自己公司还安全。丢了坏了，微软陪。
    

## 与其他类似东西的区别

本质上来说，考虑到你的智慧，数据集市，是一个战略数据库。

与其他类似东西的区别，包括：DataFlow，DataSet，数据库，数据仓库，Power BI 有啥区别呢？

DataFlow 是一个管子，定义了数据应该怎么走，管子可以套管子。

DataSet 是家里小院里的池塘。归从属的 Power BI 用户所有，一人一文件一个。

数据库是一种技术称呼，任何一片水都是数据库，从小池塘到胡泊到海洋都是数据库。

数据仓库是企业建立的统一的水库。

数据集市，是从数据仓库或数据库或任何小水塘子把水聚集到一个大池子里，是小区的公共游泳池。归小区物业管。以后谁要来里面游泳或接水，可以交物业费或免费，随你说了算。

那么小区的游泳池可以不做游泳池，做一个钓鱼池吗？可以的。业务不同，定义不同的业务逻辑即可。有了小区的游泳池，不影响家里后院的小池塘还是那个小池塘。

说明了什么？

水库，不归你管。家庭后院的水塘子，也不归你管，归用户。而谁能成为小区物业，谁就真正可以以各种名义去做各种事情了。例如：检测一次，收多少钱，每天要检测，要持 72 小时报告才能开会等等。都可以定规则了。那么，是不是在小区，游泳池子或钓鱼池子归谁，谁就很厉害啊？

## 什么样子的

如果你熟悉 Power BI，那很容易。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhriaOTw9A2jrTV4vKadXSDkqFicctXRWVghdn8SbcgDlibSSLbicIUIORagw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

主要的痛点就是：你不用等数据工程师了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhr5IDQ5jpbL5Q7W2d4n2Q8nGqiconYiblfZhFEkoSbDfl0TVL4YgGqTwpA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

建立数据管道完全是图形化的，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhrPXwwTRqkxLPRvC6w54SnzbNaHRMnCPmrJdm9ricibYpAHAF3IJ93hF0Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

要注意，这里存储所有数据，是所有。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhric3pJ7dEUEPDT2Pu0X6UblrdNSQXVabPibx2UcmQogcUVSIQMmaUZ1Dw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如上图，所有数据都流入了池子，你可以根据你的欲望来处理这个池子。

一切处理都是图形化的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhr9ibBfX0WoIPF1hrVKyj81ejdDE7PeOmUrZZSQ6PT8koI4ZaibOEia1aicQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于数据量级，不用担心：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhrBtViblEARKFiavfxfqkiaYibJzARrU5muSjryzS9Beh20ZqWyxJ0J3SoWA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果能处理 TB 级，这个规模完全够了。

一样可以做出 Power BI 级别的可视化报告：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhraMeBuTT6zDySBkLJBER82YucANCPHyqIF3JzpLxPBfqCBecSyZutAg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

建立数据处理的逻辑完全不需要写代码，如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhrL8nZyQxXQ2OfiaQ96pToRbib6vTDM0syhnfuMEbOPZGk2eKO6BEVZnDg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 什么时候可以用

那么，什么时候可以用呢？现在。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhrx4Zv50J1rVLgcIJYszz35aXWibApiaH4jgpO7FibANMzpXiaUv3icW5v8Zw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

获取数据后，还可以设置增量刷新：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhrsGAKzDxKvvqTia2kWosDcFcQ98BKDicxapUpA1FTepHiaQSTPW2icoNkiaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以建立连接：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhrszRaskV7S30bUtemNpHl0SBocjazQaXsVyDyVZLTjnNrfia6ZPHaTGw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以构建关系模型：

还可以写度量值：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhrBLJZ0ZSh8PQK8g4dWc9er1fkFrS3EXTzfjQXSERFUD85rFEibLHqSQQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个体验和本地的 Power BI Desktop 里是一致的。

然后直接构建可视化：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOOdYqTwib2PaD4ibNzXJfGhrLDjUyVXXUnFkicobwyEyG2icorfJ4K5cs6PwZhlZ8DPr1owjXYrmSjPg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

整个过程，无需软件，666。

## 总结

很多人说 Power BI 是一个数据可视化工具。没有错，盲人永远只是摸到大象的屁股而已。况且，还是一只在不断长大的大象。你可以骑上它，也可以被骑上它的人踩死，而你却不知道。

没有错，以上一切，不是构想，已经在那里了。打开，点击，实现。

想骑上这只大象却不知道怎么入手？

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月01日 20:00 直播

Power BI 案例赏析

视频号

**Power BI 终极系列课程《BI真经》**

[

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

点击“阅读原文”进入学习中心

**↙**
