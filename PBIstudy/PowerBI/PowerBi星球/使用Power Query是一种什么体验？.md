---
create_date: 2017-12-25T20:49:22 (UTC +08:00)
tags: wx/pbi/PQ数据处理 
aliases:
pagetitle: 使用Power Query是一种什么体验？
source: https://mp.weixin.qq.com/s/SXbtAX1m0P6PLV1bp6UZIg
author: 采悟
status: 已完成 
category: 浏览文章 
notes: false
ZK: Origin
uid:
---

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOfJXWwL80c2nliaibtEPfx6hSjjsLzaaKIt54xpwpKdOFJv94dQ3eB6eg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 你和Excel高手的距离只差了一个Power Query！！！

先思考一个日常工作中常遇到的问题：如何将多个工作簿的数据合并到一张表上？

可能不同的人有不同的做法？

> 普通青年用万能的复制粘贴  
> 二逼青年网上百度VBA代码一键汇总  
> 文艺青年找个崇拜自己的实习小MM帮忙

其实都不必这么麻烦，我们无需借助高级的数据处理软件，无需学习复杂的VBA语言，无需挖空心思找别人帮忙，超级强大的工具就在我们身边，就在我们天天使用的Excel里面，那就是Power Query！

下面来看一下PQ是如何汇总多文件的数据的:

> 假设有一个连锁型零售商店，有北京、广州、杭州三个城市门店，总部每月需要汇总每个城市门店销售明细数据，现在需要汇总2016年1-3月的销售明细，共9个工作簿，保存在一个文件夹内，结构如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOAXvD1X6QEtPPdyhDHVZ8fslzuhJ4II7efNO55shuFHoCr0y33kngnA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

由于只是数据处理的过程，下面的演示就在Excel2016进行，使用Excel2010、Excel2013的插件以及在Power BI Desktop中的操作也都是一样的。

首先我们新建一张空白Excel工作簿，点击"数据"选项卡下"新建查询"，从文件夹获取数据：
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOicV92FyRQHno04XYGdCRoeYx5EJdp7VLOPZzeGEp54rDc5zgngUAticA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOicV92FyRQHno04XYGdCRoeYx5EJdp7VLOPZzeGEp54rDc5zgngUAticA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
浏览找到该文件夹的路径，确认后出现这个界面，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOg1DFibNTpDXia2TIanLIXvoceCaibv7GztZc8icrAfePgia038FhYfPPWow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击"编辑",进入查询编辑器：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOMX1bOIosiaT2pYdICuR3PHxDVIjTTY8lPkjYRWo6btqJW3tKcMjHPOw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

数据就储存在\[Content\]列,其他列都是每个工作簿的信息，现在要做的就是把Content的内容提取出来，点击"添加列"选项卡，添加自定义列，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOU0zC7tgZrLYf8QEceyQswpA6Y8gyVWO47jS3KrJTL2IXf09Xx4LuTw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

自定义列中输入公式===Excel.Workbook(\[Content\])，这里要注意严格区分大小写，不能写错了，这就是提取Excel格式数据的M函数==（关于M函数后面会单独介绍）。

确认后就出现了一个自定义列：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOuHsKE0y5hb3XV9ePFU3ojnG8nN5RXKoZibCicmGEJoQ3bGxndzZcDFjw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击自\[定义列\]右上角的双箭头展开数据，出现这个窗口，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbO5bBxpj9uDHsjt9GI07CBVm0srOA94G1AZIbcZSwsSEHic7oXWl8Z9Fw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

直接点击确定，出现了如下这个界面：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOPGHdKVhHq1W29zFHY7oHW4uPZG2rscBvcOuI9GwvicZCEtQuribEbbAQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

又新增加了几列，继续点击\[自定义.Data\]列的右上角的双箭头，然后还是直接点确认，数据就全部出来了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOOoMecjtyviaBOK3uibao3G0RaQZYX7ib2Q5HAL3uEkFupicGuhuTOBOiaRg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后只留下下各门店上报的数据了，可以看到列的标题是系统添加的，其实应该用第一行作为列的标题，我们直接点击"转换"选项卡下的将第一行作为标题：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOe4LUiaG2FVicuNXQOC0kXnfpGESNQqyqVjVw9uOnELibrxicw2NJNibYWVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后标题就提升上去了。

数据导入过程中9个表格的标题行是重复的，另外表格中可能有空行，所有把标题行和空行筛选出去，像在Excel中一样，点击城市的倒三角，去掉这两个勾选：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOkapDibmqtEZoicxn0daJDDFmy9iauyscnUqmjWHibmMibE3jkKLnib3V6C7A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

数据汇总完成，点击上载数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOIYjQ0FyojkQ8EdZchYhbOZK8Ev3IDOBBA4s63rhYIEMibsJpE0T85p2bbnHuBPj7ibW3JefX2ZW6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后大功告成，数据就全部汇总到这个Excel表格中了。

看着好像步骤挺多，其实动手做起来，所有这些步骤只需一分钟而已，中间除了那个简单的M函数，一直都是点点鼠标，是不是非常简单呢。

**更简单的是，上面操作的所有步骤都被记录下来，下个月销售记录更新的时候，比如把各个门店的4月份的明细数据放到相应的文件夹里面，连点鼠标都不用了，直接刷新数据，然后4月的数据就全部汇总到这个表格了。**

如果你说这些其实通过VBA或者简单的复制粘贴还都可以做出来，那么如果有100家门店，每家门店全年12个月的数据呢，复制粘贴显然不现实，如果数据量大用VBA估计也会把电脑卡死。而在PQ中呢，就是打开文件点击刷新，这个文件夹下无论多少文件，无论数据量有多大，汇总也是秒秒钟的事情。

**这体验爽爆了吧:)**

这只是举个简单的例子，实际上Excel能处理的工作，PQ都能处理，并且能更简单、更节省时间的处理；而Excel处理不了的大数据，PQ同样能够轻松应对。

Power Query的优势:

-   操作简单，即使是小白，无需掌握复杂的函数即可处理大部分数据处理工作
    
-   数据量无限制，具体多少取决于电脑配置，上亿行不是问题
    
-   自动化，处理过程全记录，每次数据源更新后刷新即可，无需重复劳动
    

数据处理一般可简化为三个过程，数据获取、数据整理、数据丰富，后面几篇文章会分别介绍。

动手才是最好的学习！案例数据可在本公众号回复“PQ体验”获取。


