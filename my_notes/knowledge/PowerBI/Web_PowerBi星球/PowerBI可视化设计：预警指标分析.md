---
create_date: 2022-09-18T23:27:20 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: PowerBI可视化设计：预警指标分析
source: https://mp.weixin.qq.com/s/eH8fqhSC3_bQ8FG4etP6Xg
author: 采悟
status: 已阅读
category: 精读文章
uid: 
---

今年可视化大赛最佳展现创意作品中有个设计是预警分析，最近被很多人问过这个是如何设计的，效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNgksIPrqdy8yZFRncqBz9WCmFqqVozkwLTUppf8CleAYGHo0xSfRvc7Qphc0US3XrpnQx2K1OxiaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

报告链接：https://app.powerbi.com/view?r=eyJrIjoiZTEwZmU5NmMtYmVmZC00ZjkyLTlhMzktMGUyZTM5YWVjYWE5IiwidCI6IjdlMTczODMxLThkZDYtNDlkZC1hY2Q1LTljZTY3ZmQ1ODM5MCIsImMiOjZ9&pageName=ReportSection1f9122da2a5df5047d82

这里就尝试用PowerBI星球的案例数据，来模拟做下这个效果。

获奖作品是对连续3个月同比下降的指标发出预警（如何统计连续3个月同比下滑，可参考：[Power BI数据分析：如何快速找出连续下降的数据？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076198&idx=1&sn=eea955681fca17208105e264274e795c&chksm=8e0c5471b97bdd67ddbc7337636087b4daac68539c64ee71e012f10238442fe6bf07366bd2f5&scene=21#wechat_redirect)），具体预警指标的细节，以及什么条件下开始预警，这个取决于具体的业务情况。

这里简化处理，按照<mark style="background: #FF5582A6;">低于某个阈值就发出预警，假如有三个指标：销售额、利润率和订单数量，如果某个月份，销售额低于15万、利润率低于39%、订单数量少于1000个，则预警提示</mark>。

下面是实现这种预警分析的一个可视化设计思路。

#### **1\. 指标参数化**

先写好这<mark style="background: #FFB86CA6;">三个基本度量值，然后利用字段参数，将这三个指标参数化</mark>：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNCK6CTLFN4mPcEODgJtLmYNDWaVQcbDEN3icAiarjGgywWm2O1xYy0FUFx6Mqq1jbe9moctgzBOYCw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于字段参数的用法，请参考：[Power BI字段参数介绍以及常见应用场景](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080273&idx=1&sn=b985ea8a53854f41a1ba75c0585cb3cd&chksm=8e13a446b9642d5085b1590f38ca7dd36c085269ae2d5d0fe75e09c57fc1ae270158d15d79db&scene=21#wechat_redirect)

#### **2\. 制作钻取详情页**

利用<mark style="background: #FFB86CA6;">第1步的参数作为Y轴，产品名称作为X轴，做个柱形图，作为详情页</mark>（关于详情页，你可以根据需要放置更多图表，这里简化处理，只展示一个柱形图）。

并将指标参数放到该页面的钻取框中：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNCK6CTLFN4mPcEODgJtLmYNXkQotLeGyI0icmrbyOVUUDo66ibT0Vh8ZcqQLBeRsj97eKfZSJ9Q8Yg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于钻取请参考：[深入了解Power BI的跨页钻取功能](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069310&idx=1&sn=7097550bfc21942b1120b613a5acd2f1&chksm=8e0c4969b97bc07fc38f6f19716b9df7b6505d9ae57785a8152297b28dcf8c3bb832cc0da928&scene=21#wechat_redirect)  

  
#### **3\. 设计预警页面**

前面2步是基础工作，这一步才是设计的重点。  

首先<mark style="background: #FF5582A6;">用字段参数的指标来做个表格，右键设置参数显示为“显示所选字段”</mark>，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNCK6CTLFN4mPcEODgJtLmYvj40qkjkGGRaRc0CXVS4VEfo2tFFKYq5kswTsWRjI7Srw7Lughu5Bw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后各指标就显示为列表的形式：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNCK6CTLFN4mPcEODgJtLmYhoVbFXe7v6L3GibcQMwIjZ1vVvorXO8gsSxsbROCvZVSDwDzbnhyNQw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后<mark style="background: #FF5582A6;">写个度量值来筛选这些指标，利用之前确定的预警逻辑</mark>：  

> 预警指标筛选 =
> 
> SWITCH(
> 
>     TRUE(),
> 
>     MAX('参数'\[指标\])="销售额"&&\[销售额\]<150000,1,
> 
>     MAX('参数'\[指标\])="利润率"&&\[利润率\]<0.39,1,
> 
>     MAX('参数'\[指标\])="订单数量"&&\[订单数量\]<1000,1
> 
> )

这个度量值的逻辑是，<mark style="background: #FF5582A6;">如果当前行是某个指标，并且该指标低于预警值，则返回1</mark>。  

将该度量值放到上面表格的筛选器中，筛选只等于1的数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNCK6CTLFN4mPcEODgJtLmYnCSoz4avMBwK9Hu0Rsup8HWIibhEK9kib6DKg7H6RqSn6oNzFQ2NP5jA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就会只显示达到预警值的指标列表。

可以直接右键某个指标，来钻取到详情页：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNCK6CTLFN4mPcEODgJtLmYYicTmuwl0XPuVtibxNqLyUFdJMSKCUMfRF9uG1lTVePsy5yYHnrlCstw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按照获奖作品的做法，是添加个按钮来实现钻取，这里也用按钮的做法来设计，在表格旁边添加按钮，<mark style="background: #FF5582A6;">设置按钮的属性为钻取</mark>：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNCK6CTLFN4mPcEODgJtLmYfZ3VuSibgGTqicfSN1keBBRTVKBuQnM3qk5xXDAdJ49w56RxA9XQZrNA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参考：[PowerBI交互技巧：利用按钮实现跨页钻取](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073883&idx=1&sn=0ff2967115951c9c3c440bbd6a205071&chksm=8e0c5f4cb97bd65adf01f33bcc3a8b58063cb48227702ce2d43b2df05cffda7787d97ac74a80&scene=21#wechat_redirect)

你还可以调整按钮的格式，设置默认、悬停、禁用等不同状态的格式。

然后还需要<mark style="background: #FF5582A6;">统计预警指标的个数</mark>，写个度量值如下：

> 预警指标数量 =COUNTROWS( FILTER('参数',\[预警指标筛选\]=1))

用卡片图显示出来：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNgksIPrqdy8yZFRncqBz9WQiculXKNrmUXZ4xFzUZHSianOKYV2sJaKSePCTjpUzeciagBYQ6oMkOuQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就将预警的可视化做好了，剩下的就是<mark style="background: #FF5582A6;">建立书签，将按钮设置为透明，叠放到卡片图上方，来切换是否显示指标列表和“查看详情”按钮的书签</mark>就可以了，具体做法可参考：[利用Power BI的按钮和书签，动态切换图表](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068244&idx=1&sn=4395dc8163cded6a268dd65c3583157a&chksm=8e0c7543b97bfc5551a6626667fccb71b36b303777be57cb0339f3138d2761c43b707a01c073&scene=21#wechat_redirect)

最终效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNgksIPrqdy8yZFRncqBz9WVe2oROibRwCnHYGd0gz09ggU7tfejFIE2TVelqZl4mzrd9uWsSMGNEw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

以上关于预警分析设计的细节也许和原作者的做法不同，但可以实现同样的效果，关键是要打好基础，灵活运用书签、钻取以及字段参数等各种功能的用法。
