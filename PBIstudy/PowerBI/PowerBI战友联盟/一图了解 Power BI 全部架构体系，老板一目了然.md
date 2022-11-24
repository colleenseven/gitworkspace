---
create_date: 2022-03-16T13:26:56 (UTC +08:00)
tags: 
aliases: null
pagetitle: 一图了解 Power BI 全部架构体系，老板一目了然
source: https://mp.weixin.qq.com/s/pZx4kjfUuA3vbrfErUV0Og
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

很多小伙伴的企业已经引入了 Power BI，想知道 Power BI 整个架构是怎样的，也方便给老板做介绍。

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LNaATN7WjohI5AwhwkBtY5CHuiack6QOsSFgiaUDAjDZZCXA84P2YicnhXicGtjufR8uK5EI4YTWbdQwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

从 2015 年 7 月发布以后，经过近 8 年的迭代，Power BI 的整体架构已经稳定，这里参考 Dustin 绘制的架构图给大家做一个介绍。小伙伴可以在作者的网站下载高清版 PDF。

## 用户角色

将用户角色分为两大类：

-   IT 型，以负责技术实现为主要目标，强调更高，更快，更强。
    
-   业务型，以负责改善商业分析为主要目标，强调更准，更赚，更优。
    

又具体分为一些小类：

IT 型的角色包括：数据分析师，数据工程师，程序员，ETL 工程师，大数据工程师，算法工程师等。

业务型角色包括：业务分析师，需求分析师，终端用户，老板等。

## Power BI 体系

Power BI 以 Power BI 桌面端为代表，是一个完整的体系，从支持一个人的数字化工作到支持一个跨国大型组织的数字化工作都提供了良好支持。具体到各自的公司如何使用 Power BI，并非买得越多越贵越好，要根据自己的情况和现状选择合适的组合方式。

但一般说来，从企业中的每个人使用 Power BI 桌面端总是一个好的开始。

## Power BI 桌面端（Power BI Desktop）

用户：老板，需求分析师，终端用户，业务分析师，数据分析师。

从企业内外，云上云下收集数据，设计 Power BI 报表并发布到云端或企业内的报表服务器。

如果个人或团队使用，则可以作为分析工具，免费使用，无需发布。

如果企业使用，且数据可以上云，则可以发布到云端使用。

如果企业使用，且数据不可上云，则可以发布到企业内的报表服务器使用。

无需购买，永久免费，可在官方下载，或者在 excel120.com/#/pbid 高速直接下载。

## Excel

用户：老板，需求分析师，终端用户，业务分析师，数据分析师。

从企业内外，云上云下收集数据，设计 Excel 报表并发布到云端或企业内的报表服务器。

如果个人或团队使用，则可以作为分析工具，无需发布。

如果企业使用，且数据可以上云，则可以发布到云端使用。

如果企业使用，且数据不可上云，则可以发布到企业内的报表服务器使用。

随 Office 365 安装，推荐使用 Office 365 订阅版。这是数据分析是世界标准。

注：Excel 是 Excel，电子表格是电子表格，用 Excel 可以从基础到高阶更深度地玩转电子表格，听得懂表示听懂了。

## SQL Server Data Tools / Report Builder

用户：数据工程师，数据分析师。

设计分页报表或分析服务。

如果企业使用，且数据可以上云，则可以发布到云端使用。

SQL Server Data Tools 已经与 Visual Studio 集成，可以直接使用 Visual Studio。

Report Builder 设计分页报表已经日益成熟并与 Power BI 云端更好集成。

分页报表与普通报表的区别在于：

-   分页报表，可以做到参数化，像素精准也多页导出 Excel，适合数据明细密集型的多页报表。
    
-   普通报表，可以做到可视化，强调汇总型的可视化交互分析，适合在汇总级分析问题使用。
    

微软官网免费下载，用于构建 SQL Server 分析服务或分页报表。

## Power BI 报表服务器（Power BI Report Server）

用户：数据工程师，数据分析师。

在企业内网环境承载报表并向企业内提供服务。

无法单独购买，需要购买 Power BI Premium 或 SQL Server 企业版后附属携带该套件。但可以在其免费评估期试用。

## 数据网关（Data Gateway）

用户：数据工程师，IT 管理员。

定时将企业内数据同步到云端的中间桥梁。

微软官网免费下载，在 Power BI 桌面端采用发送云端模式下，与云端配合使用。

## 数据流（Data Flows）

用户：数据工程师，数据分析师。

在云端运行，将云端数据分层整合形成数据的基础架构，供后续分析或应用。

可在 Power BI 云端使用。

## 数据集（Data Sets）

用户：业务分析师，数据分析师。

在云端运行，以表和关系为基础构建的数据模型以及其上定义的计算逻辑层，为可视化或报表提供分析基础。

可在 Power BI 云端使用。

## 报表（Reports）

用户：业务分析师，数据分析师。

在云端运行，基于数据集构建的可视化图表的集合，用来分析业务中的问题。

可在 Power BI 云端使用。

## 仪表板（Dashboard）

用户：业务分析师，数据分析师。

在云端运行，从报表中提取直接用于监控业务重要 KPI 的看板。

> 注意
> 
> 报表和仪表板更多是逻辑上的叫法不同，其本质元素都是基于数据集构建的图表。

## Power BI 高级版（Power BI Premium）

用户：数据分析师。

在云端运行，专门用于单独承载 Power BI 服务。

分为：

-   按个人订阅，可按个人购买，用于单个用户。
    
-   按容量购买，分为不同等级，根据企业需要，购买不同量级。
    

可在 Office 365 管理员界面购买，可联系本组织 IT 管理员购买或让该管理员联系微软客服咨询购买。

## Power BI 嵌入式（Power BI Embedded）

用户：程序员。

在云端运行，专门用于承载 Power BI 服务中的数据集部分并对外提供编程接口，实现企业 OEM 定制化。

可在 Azure 中购买，可联系微软 Azure 客服咨询。

## 终端：手机端

用户：终端用户。

在应用商店下载：Power BI App。

## 终端：第三方应用

用户：终端用户。

参考第三方应用的说明。

通常，第三方应用通过调用 Power BI 嵌入式编程接口提取内容与相关应用整合形成整体解决方案提供给最终用户。

Power BI 的成分是透明的，用户感知不到 Power BI 的存在，甚至不知道 Power BI 这个名词，但用户却正在某些场景中透过第三方应用使用了 Power BI 的能力。

## 终端：浏览器

用户：终端用户。

国际版，可以登录 app.powerbi.com

由世纪互联运营的中国版，可以登录 app.powerbi.cn

## 终端：Excel

用户：终端用户。

在 Excel 中，获取数据，连接到 Power BI 即可使用使用 Power BI 提供的服务。

## 总结

以上架构已经非常稳定，该架构图最后更新于 2019 年，但仍然反应了 Power BI 目前的实际状况。

如果正在考虑向公司其他小伙伴解释 Power BI 的构成以及云上云下各种相关成分，那么这个架构图以及这里的名词解释，用户定位，以及是否收费或购买方式可以参考。

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，可以直接下载本文架构图高清版。

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
