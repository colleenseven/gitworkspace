---
create_date: 2017-12-21T20:47:45 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases:
pagetitle: 认识Power BI
source: https://mp.weixin.qq.com/s/u5c-7sG0SI4rSjw-3EJQ8g
author: PowerBI星球
status: 已完成
category: 浏览文章 
notes: false
ZK: Origin
uid:
---

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOMoT2prsVic5ZfEGZVunkM0CVlbPFLEVwhwA8FtDHF0ia7p9OYtwa5rpxUEGfic8IVFuq1nEMPdbM6w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

> 本文简单介绍什么是Power BI、如何下载安装PowerBI Desktop以及PowerBI的界面和操作的一般步骤，现在就来迈出我们学习PowerBI 的第一步吧。

___

**Power BI是什么?**

Power BI是==微软推出的数据分析和可视化工具==，我们先来看看微软官方是怎么介绍的：

> Power BI 是一套商业分析工具，用于在组织中提供见解。可连接数百个数据源、简化数据准备并提供即席分析。生成美观的报表并进行发布，供组织在 Web 和移动设备上使用。每个人都可创建个性化仪表板，获取针对其业务的全方位独特见解。在企业内实现扩展，内置管理和安全性。

简单来说就是可以从各种数据源中提取数据，并对数据进行整理分析，然后生成精美的图表，并且可以在电脑端和移动端与他人共享的一个神器。  

PowerBI包含桌面版Power BI Desktop、在线Power BI 服务和移动端Power BI应用，我们学习的时候使用PowerBI Desktop已足够，这个是PowerBI的精髓技能，简单来说PowerBI服务和移动端不过是PowerBI的分发共享功能而已，好消息是，PowerBI Desktop还完全免费。

**如何下载安装PowerBI Desktop？**

登录微软PowerBI主页：https://powerbi.microsoft.com/zh-cn/，

从产品中选择Power BI Desktop:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amouoanib6XibbWviaPIe0llpKj8iaDKCZXzBhtf2HF3ggy3TmlNMbw36TD40fw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下载的时候选择高级下载选项，可以选中文版本（如果英语不错，也可以直接下英文版本的），根据电脑的操作系统选择32位或者64位的安装包。 

如果是WIN10系统，还可以直接在微软store里面找到Power BI Desktop应用直接安装。  

安装完成，启动后会提示你注册登录，暂时不想注册直接关掉就行，如果注册，推荐申请个126邮箱，很容易注册成功,现在注册还可以享受2个月的PowerBI专业版体验。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amouoe1ibbM4u1D1MPu2cMJtS9RKeibj6FNiaOeeJOaibYsdO2x7piaeNxLTSdRA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**如何使用Power BI？**

进去后界面如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amouoLFqgebkiaZ2XUXTD9SKx8nSDnt67WmjicmlkDrtzOnkdUvibqZ3X9mxfQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

数据处理的第一步就是获取外部数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amouotOo6N8H0J7KID5L4lVaZH1BtCBfGve7lPgva65P7icpibObStbcfArvQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amouo4nmC3l70kcNFB1JNDeBOj3zfVUf2cCy4icHonr7W3Y3JqfdmZNCcjzA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

常用的数据格式如excel、sql、csv/txt出现在最上面，如果是其他格式的，点击更多，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amououOibJk4A1NkCVJyNJyC1Z7ygxgwycibE0ictMtqiaCVXSOKiau5ib0fCbTtw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

 出来很多可选项，基本上目前所有能见到的数据格式都可直接导入。 

数据导入后，可以进入内嵌的查询编辑器，这是Power BI的一个主要模块，也可以称为Power Query，数据整理都在这里完成，后期会专门介绍。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amouonJfcrSIcSWLSicRt4Ywic4CHrvUXqHv73xXscRWIF1AHmr8ryXEUgm3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

整理后的数据进入数据建模，不要被建模这个词吓着了，其实就是表格之间建立关联，这是我们下一步数据可视化的基础，当然如果只有一个表，就没有必要经过这一步了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amouogOaZW09uyTJpJfUNrff8Mp49e3bsOe8frvZZPuiaTddCfdH4x92MVicA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就可以进行可视化工作了，来看看可视化的组件：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amouoYVr80j45iay441ibGVNDS0K6JhT5HBodtUhLWW3e7noASrJyjaB8kibibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里显示的是系统默认自带的图表类型，平时常见的图表都有，另外推荐PowerBI一大理由就是还可以加载更多的自定义可视化包，各种酷炫图表，比如这些：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMj6y3eHibjtCG6Uk52amouofvQ4sVG52rAFgGq8Mc5rauXK9SAEqq2ymjkOAzlEaV9teTvf7OZZ0g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

目前已经有100多种自定义图表可供免费下载使用，还在不断增加中……

今天就介绍到这里，现在就安装PowerBI Desktop，开始我们的数据探索之旅吧。
