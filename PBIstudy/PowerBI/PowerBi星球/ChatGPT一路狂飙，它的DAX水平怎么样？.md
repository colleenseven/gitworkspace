---
create_date: 2023-02-09T23:32:54 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases: null
pagetitle: ChatGPT一路狂飙，它的DAX水平怎么样？
source: https://mp.weixin.qq.com/s/gNC_H4ELaKFW1rESaIxQvA
author: 采悟
status: 已完成
category: 浏览文章
notes: False
ZK: Origin
uid: 
---

昨天体验了一下ChatGPT，聊了一些PowerBI的问题：

[体验ChatGPT，我和它聊聊Power BI](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484083606&idx=1&sn=cd9df4ce8bf217b41d0787bb48b043fc&chksm=8e13b141b964385757882edd5011447b43877a4156ced9dc248609074d93747da436c6cdee7b&scene=21#wechat_redirect)  

很多星友问，既然ChatGPT这么智能，可以帮助写DAX吗？这篇我们就来和ChatGPT聊聊DAX的话题。

下面先和它随便聊聊DAX的概念和原理等话题，然后再从易到难来测试一下它写DAX能力，通过它的回答来感受一下。

___

**DAX是什么语言？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etQlB3w9e0icCicnV9lC85QXzIia6DTb8UHsqn1WJKC8QFhialkibiacrDAV7g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**DAX语言与其他编程语言最核心的区别在哪里？**
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etgGDxhtejRNDR6aaI7ZUuIQRaT43bLfBlOIpWXp5VpBtRGYbibtswo6Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etgGDxhtejRNDR6aaI7ZUuIQRaT43bLfBlOIpWXp5VpBtRGYbibtswo6Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
**DAX的底层核心原理是什么？**
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etldoX22uIC8To4TrLTFt91rBuvzWvbJeM9lJ0KV2hJSChtpSxic38YIQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etldoX22uIC8To4TrLTFt91rBuvzWvbJeM9lJ0KV2hJSChtpSxic38YIQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
**如何快速理解DAX计算逻辑中的上下文概念？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9et3N4Odics6beye9lvPU6m6zykBwgibyGRsibFZlXRUPRViaeIId1TZ1VZUQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**DAX优化策略有哪些？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etyOhykxHh1nJH1JVFK5qR1LUZ4Es5WBibzwSQBe2QSgAnGLjIhzajgHQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

从前面的回答可以看出，ChatGPT的逻辑性很强，什么问题总能总结出一二三，如果你熟悉DAX，可以从其中的套话中找到部分有用的点，但是如果你完全不熟悉，通过这些回答，并不会让你更理解DAX，看完应该还是一头雾水。

**DAX之父是谁？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etYa5Dgtd5ib9rVojkrPOBbtfejMB31v5ZWO6346Mfqs6GqBKsicsv35Ww/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

原来ChatGPT也会犯错，把意大利大神当成了DAX发明者，估计是因为这两位顶级大神在全网对DAX的贡献和分享内容最多吧。

**如果我见到DAX的设计团队，并有机会向他们提出一个问题，你觉得我最应该问什么？**  
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etXDkiawTaDRI7RacJPic1DmIENdAVNqWpQMuR40n4hmdUkBjtUZMMclcQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etXDkiawTaDRI7RacJPic1DmIENdAVNqWpQMuR40n4hmdUkBjtUZMMclcQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
嗯，如果真的有可能见到，从这些问题里选一个向他们提问:)

**DAX中最重要的函数是哪个？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etCsA1Qst9kiazC5EnJasrCveH4sOgGvkZiaGXrRyl4RuUlotDMkqo1iaJw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**如何掌握CALCULATE函数？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9et2Ay89XpyUicd36oVuCYVKQyFYqEWk9G4uhlPd1qvXMKvkG0tfcwk56Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

正确的废话。

**2022年新增加的DAX函数有哪些？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etyyHr7ALbLxEX3QibZIC8TH8BQlra4wxsbZCa6NDMicMib53K0vUiciaIicaA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

ChatGPT关于DAX知识还停留在2021年~

**如何在一个月内精通DAX?**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etHHQjyc3NHIhWjATaicy4VafJEicrIZWkbsBE6OsarJJ5Wzx4pzsNETKA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

看起来很鸡汤吧~

**请给我推荐一本学习DAX的中文图书？**
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etEtTnvgAWzOKVD7ibHSOvpjibKcptrfG0iaFeLRo9Y0tUBbN9BSwic6zbxA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etEtTnvgAWzOKVD7ibHSOvpjibKcptrfG0iaFeLRo9Y0tUBbN9BSwic6zbxA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
这个问题ChatGPT不但犯错，竟然还不承认？  

**我在工作中会用到PowerBI，但是不想学习DAX可以吗？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etyuTSbYr4BqIgNbxCCBDXHib0ozPlBqN6ibcHN8SEkvFrfHCyicGpGzAsQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**你可以帮我写DAX公式吗？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etlyiabyibRvD0VdyiczpbbibiamaILfTQpMBqthdRp48D2EceuDywTXYHPSA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

既然ChatGPT这么自信，那就试试来写DAX吧，先从建立模型开始。

___

**假设有三张表，订单表（包含订单编号、订单日期、产品名称、销售额等字段），产品表（包括产品名称、产品类别等字段）以及日期表（包括日期、年度、季度、月份、周等字段），在PowerBI中如何建立一个好的模型？**
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etmEMhTicn8GvOOzsXSmAlt9n0JYnt2Ox0ibOaLvlq95SDGhUgORY7jWfQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etmEMhTicn8GvOOzsXSmAlt9n0JYnt2Ox0ibOaLvlq95SDGhUgORY7jWfQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9eticibeIWaoXdx1L1LzI53Btia6GnXibWA3WGDkRTQ3onIURoVHSj3uMKNNA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

废话太多了，建立个关系依然还要总结出这么多点，关键有些还是错的，比如建立模型应该到“模型视图”。

**我需要使用PowerBI分析销售额的同比变化情况，请以上面三个表组成的数据模型为基础，如何实现同比分析？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9et9DCfh68RdUyGYQDglcFu85yibfHLQXy2unmIfjhUca4exwQHQZ2C1jQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

真的非常详细，把操作步骤都列出来了，同比度量值也还算正确，不过需要注意的是，变量名是不能使用中文的，你不能完全照搬，你直接复制到PowerBI中使用肯定是报错的。

也许是用中文解答，ChatGPT把本来是英文的代码自动翻译成了中文。

**如何计算出每个产品的销售额排名？**
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etz2AT5cIW1ktkfxuS4kzpYorsBZNQUAug2W8IS6fxzgVhR4o9ciaba4Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etz2AT5cIW1ktkfxuS4kzpYorsBZNQUAug2W8IS6fxzgVhR4o9ciaba4Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
ChatGPT这个解答也还可以。

下面换个复杂一点的分析。

**以上面的模型为基础进行数据分析，请给我写一个销售额60天移动平均的度量值？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etFVz8lns2IPRvDPmGCNM33NvpfFAxvCIhTQTDiaI9iaLQoVEQ2ork0ZAg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etFMyyPFMv0OybymJHmeRSuXYqCzZ6qyq7m1Q5HiaKRt9jJH3OQibAOnzQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于写法就太扯了，问题理解有出入，并且DAX并不存在的函数都冒出来了。

是不是因为我的提问太简单了呢，我再详细描述重新提问。

**我需要使用PowerBI进行60天移动平均的计算，请以上面三个表组成的数据模型为基础，用DAX函数帮我写一个60天移动平均的表达式？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etNU4meHq5eiaIVNRXVEH8WZLlI2icnDpEyPkMmCZM7Y8LiaZHOa3INH3oA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这个写法还算可以，基本可以实现，但为什么没有以上面的模型为基础呢:)

**上面的表达式如果用DAX时间智能函数来优化，应该如何修改?**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etbI6AiaNFia6FXaO1HteAEXujRib0hnKnql7nTY8c7ianjB2F3IYWYmrZSA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

ChatGPT又乱了，这个公式完全不能用，可以看出它对时间智能函数并不是很理解。

**我需要使用PowerBI对产品进行帕累托分析，请以上面三个表组成的数据模型为基础，如何写度量值来完成帕累托分析？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etgHdwPsMiaM34ibMNezjlMNg7ub09BS17qpSicIkXicbe5X1cOJMTiaCq79Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9etm3xMl0lw5IA48ULWs3opJW8VcaWU5HJy7HDbn9iboia4O0WbWiclK36GA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

让ChatGPT进行更复杂的帕累托分析，更是勉为其难了，虽然它一开始理解了什么是帕累托分析，但是具体如何实现，它给出的公式是没法用的。  

通过上面几个例子可以看出，对于非常简单的基础分析，比如计算同比、排名这些问题，ChatGPT能提供帮助，不过也需要微调和修改。

但对于更复杂的数据分析，目前它还不能帮助我们写出正确的公式。所以对于DAX，ChatGPT目前顶多能提供一点辅助，想依靠它帮助我们做数据分析还完全不现实，我们仍然需要学习DAX。

当然，ChatGPT自己也知道~

**既然你能帮忙写DAX，那我为什么还要学习DAX呢？**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPIBmJComFTHTqs1n6dz9et4hmPzWTmKPgIic69GUSODy2x4qdHcggOBpd8Yeb63HoJuibhb5tWpusQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

end
