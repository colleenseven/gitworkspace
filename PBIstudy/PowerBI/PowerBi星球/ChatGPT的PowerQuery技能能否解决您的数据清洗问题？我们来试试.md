---
create_date: 2023-02-27T23:30:29 (UTC +08:00)
tags: wx/pbi/PQ数据处理 
aliases: null
pagetitle: ChatGPT的PowerQuery技能能否解决您的数据清洗问题？我们来试试
source: https://mp.weixin.qq.com/s/HP7kTraB9mNGU38DWTW5Qw
author: 采悟
status: 已完成
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

前面我们测试了ChatGPT的DAX水平： 

[ChatGPT一路狂飙，它的DAX水平怎么样？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083645&idx=1&sn=d2d0da62240aaadcb200bb7c07dfbcae&chksm=8e13b16ab964387cf6169ceb2c994bc79db50fe21ba9cf19834f719bfc137e6cc8a40e295717&scene=21#wechat_redirect)  

今天我们再来通过几个典型的问题，来测试一下它的PowerQuery水平怎么样，看看它能不能为我们赋能，帮助解决数据清洗问题。

___

**你觉得PowerQuery怎么样？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWozd6MoSNZ4YKQODW135OWicHaEIMkVC9FpLEcHlZ7NPibohFfdKIa80RQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

pq的优点介绍的还是挺全面的。

**PowerQuery中最常用的10个界面功能是哪些？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWoeiaib0rRh7xNp1WpNhkHHoMXI4jXNjCc2jDEmLD9UsOfvzJfTV6IDglQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

列出的这些功能的确很常用，看来它真的有学习过PowerQuery知识的，不过最后一个功能"拆分列"，被它说成（翻译）"分裂列"怎么那么别扭。

**如果一列文本数据中，想把其中的字符“x”,替换为“y”，在PowerQuery里如何操作？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWoWU86Bow9o3ic729zc5bppzkz4EybOB51wNA0cbVl2F5iaDCBic8AX3PiaA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于具体的某个功能，它也能进行具体的解答，并提供了扩展知识以应对更复杂的替换需求。

**如何利用PowerQuery将二维表转换为一维表？**
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWoibGvRzJmGmPcKy21rgzB7pl4ZvFBZAqiaPZXH77Iueib2MgYMpuCUmwrw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWoibGvRzJmGmPcKy21rgzB7pl4ZvFBZAqiaPZXH77Iueib2MgYMpuCUmwrw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
它知道有逆透视列（Unpivot Columns）功能来实现二维转一维，但是对这个功能的具体操作的回答并不准确（不会弹出对话框让你选择保留的列）。

关于二维转一维的操作参考：[关于一维表，你想知道的都在这里了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068871&idx=1&sn=4ab596602ed0a4c851755673d8fcf37a&chksm=8e0c48d0b97bc1c6e8edc0d31110b669c87740e55601fce30e498c9801af972ca1f366eb7ab9&scene=21#wechat_redirect)

**如何将Excel数据导入到PowerQuery？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWozksM5BBtZb8cGZ9YLibQIRLFXfdJNibqJickevoWiaBJic0dMKfNq217icIA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**PowerQuery如何将清洗后的数据导出到Excel？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWoFhibHXwYz42JXMzsic1qtvYAPuaXH7OKeqlcmLGcVreAXEkZkXbhbAhg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这两个回答大部分还算靠谱，但有一个地方不准确，PQ编辑器中并没有”文件>导出到Excel”的功能，并且它默认将PowerQuery视同Excel的模块了，而没有考虑PowerBI。

**我想掌握PowerQuery，是不是必须学习M语言？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWoeHJxdTBiaL6icnicGWULXYSpCPkChXpxKTNkxQXwrrK0yQsBMgibpWZiaXg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于是否要学习M的建议还是非常中肯的。

**如果我有数据处理需求，你能帮我写M公式吗？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWozcgpmWn271S68urgu8yIj7Pp9mKcAhENwm9UF5ibaxJ1YsoCEPbVJWw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于是否能写M公式，它给出了肯定的回答，不过留出了一定的余地，不像之前问它是否会写DAX那么自信。

**在PowerQuery中，如何将一个文字和数字混在一起的字段，比如“Kevin12345”，拆分为文本和数字两个字段？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWo5HoLmiceKqV8P3Uqp5gdOpicLwWtwCE07Jibx5DTfRksh5AiauGFeqshKQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于这个需求，其实可以直接用拆分列才实现，不过ChatGPT给出了更繁琐的添加自定义列的做法，使用了Text.Select函数，这个函数还算恰当，不过细节并不准确，问题中的"kevin"是小写，但是它给出的公式是从提取"A"到"Z"，显然是无法实现的，看来ChatGPT默认情况下也不区分大小写。

**有一列数字，PowerQuery如何添加一列，逐行累计求和？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWoDXDCa6a5rsZuYWTqttZ5tEnyOibv2e90bzZpCic2WRUWRYrhQicAWTxew/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这个看着一本正经的大段回答，其实是做不到累计求和的。

**请使用PowerQuery的M语言，生成从2021年到2023年的日期表。**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPOXRpJJEPyguKgsm2YawWojImqIn8j2GaWZg1HTia6hGGFRVQLteq7dFvQghp91TojQfrJCsz2Btg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

它对需求的理解还可以，不仅生成一列日期，还很贴心的添加年、月、日、周等粒度字段，不过如果你直接复制粘贴这个公式到高级编辑器中，肯定是报错的，中间有些公式的用法不对，需要调整才能使用。

通过上面这些问答可以看出，在Power Query的界面操作方面，ChatGPT还算比较熟悉，但中间的一些小错误需要我们对PowerQuery比较熟悉才能发现，其实这些我们通过简单的练习也能很快掌握，不用麻烦AI。

而真正想让ChatGPT帮忙的M语言，除了非常简单的情况，稍微复杂点的它也写不出来，写出来的也不准确。

与DAX一样，现在靠ChatGPT做数据清洗工作还不现实，它顶多可以提供一些辅助，我们仍然需要通过个人的学习，才能更高效地解决数据处理问题。
