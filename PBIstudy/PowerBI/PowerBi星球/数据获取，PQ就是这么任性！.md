---
create_date: 2017-12-26T20:50:02 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases:
pagetitle: 数据获取，PQ就是这么任性！
source: https://mp.weixin.qq.com/s/-_RMyKkUQWbaczWwHbztJQ
author: 采悟
status: 已完成 
category: 浏览文章 
notes: false
ZK: Origin
uid:
---

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOUOZsFibCwFS2ib6aIjFQbOKaicMPNxicd1QcRg3VFg8iaQekQ1iazdsDXic8w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> PowerBI的强大绝不仅是最后生成炫酷的可视化报告，她在第一步数据获取上就显示出了强大的威力，利用Power Query 的强大数据处理功能，几乎可以从任何来源、任何结构、任何形式上获取数据

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPibfNia9NL0GKbF9JJQUvfXXr4KEqMxqPfxXvWXvnxJB5HWXw358CrTP4TVDVp9LuHtH0ibibDmJJUfg/0?wx_fmt=gif&wxfrom=5&wx_lazy=1)

数据的获取上不仅支持微软自己的数据格式，比如Excel、SQL Server、Access等;还支持SAP、Oracle、MySQL、DB2等几乎能见到的所有类型的数据格式，总有一种适合你；

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibfNia9NL0GKbF9JJQUvfXXUrhx8D03PCG1JvXoQK3j2ibUEzs9nqtBS67d0ZHeuusb5pL9HtKOhww/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不仅能能从本地获取数据，还能从网页抓取数据。选择从Web获取数据，只要在弹出的URL窗口中输入网址，网页上的数据就可直接抓取到，用这种方法我们可以实时抓取股票涨跌、外汇牌价等等交易数据，现在我们尝试一下，比如从中国银行网站上抓取外汇牌价信息，先输入网址：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibfNia9NL0GKbF9JJQUvfXXghwF4C6C1IibOuBFTh366ciayDSTIF4GpuZbnnpKNnaN4XslnaIPfg3Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击确定以后，出现预览窗口，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibfNia9NL0GKbF9JJQUvfXXeia812aEQAM1icVmzswxU273icdzRcFdgKSQxrBoPLpRqYd9icXcG23Sfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击编辑，进入查询编辑器，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibfNia9NL0GKbF9JJQUvfXX3eQJZ8UFwrLMrv2mCXvsE3uZ7aiaEwiczv5J0ZIpoTk0Q8tyBbaWqLpA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

外汇数据抓取完成，剩下的就是数据整理的过程了，而且这些抓取的信息可以随时刷新来更新数据的。这只是抓取外汇牌价的第一页，其实抓取多个页面数据也是可以的，等后面介绍过M函数以后再专门写一篇。

以后再也不需要手动从网页上复制数据再粘贴到表格中了。  

其实每个人接触到的数据格式很有限，熟悉自己的数据类型知道如何导入到PowerBI以后，下一步就是进行数据处理的过程，这才是我们真正需要掌握的核心技巧。
