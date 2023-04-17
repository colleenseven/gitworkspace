---
create_date: 2020-09-14T20:38:37 (UTC +08:00)
tags:
aliases:
pagetitle: 手把手教你利用PowerBI实现动态TOPN及其他
source: https://mp.weixin.qq.com/s/RJ06ktWozDdZ9Z072VfoDw
author: 大脸猫
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

> 文/大脸猫
> 
> 8年汽车行业数据分析经验，擅长跨行业快速理解业务并搭建模型，利用Power BI，Python等工具实现业务及报表自动化，相比技术更关注如何落实实际业务场景的解决方案。

最近在做企业内部培训的时候，碰到一个实际业务问题：

在竞争品牌分析的时候，同事制作了一个饼图，用于显示不同品牌的市场份额。

但是他需要动态选择时间或者细分市场，品牌实在太多了，如何让图表自动显示TOP3的品牌并将剩余的品牌归类到“其他品牌”中进行显示呢？

下面来复盘一下我们的解决方案，POWER BI的迷人之处在于永远不止一种方案或者思路，如果你有更好的解决方法，欢迎分享。

为了便于大家理解，我将数据极可能的简化，避免数据认识负担。

假设我有这样一份数据，包含品牌，销量，以及年月。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFUT2Zyic82Rp9XVEfEtsOI2DYibPznX8IwTRvrYBZjGEbBQ7lB5QKGdBg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

初步制作了这样一张饼图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFnvxlQl7qNpVCwIBIm8A1qzoPLibFeQ9ZOXjCWgVViafCXcGiaOyCiaxgaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

现在想实现的目标是：

**当动态选择年月切片器的时候，在这个图中只显示出当月TOP 3销量的品牌，剩下的品牌自动归类到“其余品牌”中进行计算。**

看似非常清晰简单的需求对不对，但是实现起来是不是感觉无处下手？

我们来理清一下思路：

**问题1：动态图例问题，如何实现TOP 3品牌的显示？**

第一反应是利用筛选器，以销量作为判断基准，实现TOP 3，于是我尝试了一下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFI2Zt0dhOMW7oPMts4a2kL5usYAfnDeLb9Z5rFrqsK5nK3fH6tjXrsw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样是实现了动态显示TOP 3的品牌，但是剩下的其余品牌怎么办？

于是换个思路，我们想要动态显示TOP 3和剩余品牌，是不是可以翻译一下？

**永远只显示销量前三的品牌，再加一个品牌，它的名字叫“其它品牌”？**

让它永远显示 TOP 4个品牌，其中人工赋予“其他”这个品牌永远为最大销量？

感觉这个思路有戏，开始尝试起来。

要想实现这个效果，那我要首先建立一个含"其他品牌"的**全量品牌数据**。

选择新建表，使用Union和Values函数即可。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlF2PNdCoQvdb9kx3WpCpTDdoHZtZrVopwibhpFut41Jfmibe6ayMuLgTLA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后建立这个品牌和销量表之间的关系：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFQXOgRtYl1GAt0AuzjMKxqM3wmX7UEocgooZL8Dic6ObM5jiamdSzwYTQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

接下来做一个简单的测试：

先快速建立一个表格，使用刚刚建立的品牌字段加销量字段：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFRjb4uiaOmRqRBkFNiaWYlU9XBNBMU1LWbbJkAxNhEBR8OoaKWPicsEzfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以看到“其他品牌”暂时没有显示出来，因为它本身没有意义，自然筛选不出销量数据。

这里我们编写一个新的销量度量值TOP4品牌销量标准,将“其他品牌”赋予销售量数据，它将仅用于我们动态筛选TOP4品牌： 

> TOP4品牌销量标准 =
> 
> IF(
> 
>     SELECTEDVALUE('全品牌数据'\[品牌\]) = "其他品牌", 10000,
> 
>     SUM('分品牌销量'\[销量\])
> 
> )

这样我们就成功赋予了”其他品牌”一个销量，这个销量我们设置为不可能实现的最大值，比如10000,现在我们再来尝试一下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFHAsq7Ug3QEOUibBqc0z3STNb60kDv3ibNpwtddtib3e7FymCBZZndWFvA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

成功了，现在我们基于TOP4品牌销量标准筛选前4个品牌，成功实现了每次都动态显示销量前3品牌的名称加上“其他品牌”。

接下来新的问题来了：

**问题2：如何让其他品牌显示正确的销量？**

我的思路是编写一个度量值，利用变量先计算出TOP3的度量值，再反减出其他品牌的合计值即可：

**1、全品牌销量数据应该很好写，用Calculate + ALL。**

**2、TOP3品牌的销量数据需要用到TOPN，TOPN可以理解为一个迭代函数，迭代“全品牌数据”这张表，同时基于刚刚写的\[TOP4品牌销量标准\]，取出TOP 4的品牌（由于人工赋予了一个“其他品牌”销量值，所以在取出TOP3品牌的时候需要考虑在内）。**

**3、最后用一个IF和SELECTEDVALUE实现“其他品牌”销量的正确显示。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFdpciadT4q6REntSEHEorjMv8GR4tzdP58FbfBsDB4M8HPJaL1kh6U5Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFEIdiaoSSoAm12JlkCJF0mHp6ShvicvXVQ1GTmdb7aujslMQQ7F7rIMPw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

大功告成！成功实现了动态显示TOP3和其他品牌的正确销量！

接下来就可以将表格改成饼图啦：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFRv0tNuibzzxppgIfiauQYCfexB2SMR6fyVpy8VfgdLXg37paSNiczQHqQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这其实属于POWER BI常用的一种套路，利用度量值巧妙实现一些比较个性化的需求。

**接下来我们再来拓展一下，能不能实现动态显示TOPN品牌并自动将剩余品牌归类呢？**

要实现动态TOPN，首先肯定是要先建立一个参数表，点击新建参数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFrhMZKEswhCriaRQPWHQC6iaMlePYGcjttUwZ0cicF0rhMSSlSuqic9tZOA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

有了参数，和刚才相同的思路：

**问题1：动态图例问题，如何实现TOP N品牌的显示？**

可以翻译一下问题：如何只显示N+1个品牌，其中1个是永远排第一的“其他品牌”, 剩下的是销量排名前N的品牌？

这里需要继续借助一个辅助度量值排名了，新建度量值：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFO8ogO5MDYu5RH7B7fKQOGEUMKGjvbGA23I0CMk0YP3osicFaib0gOlAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里利用刚刚建立的\[TOP4品牌销量标准\]这个度量值，还记得吗，这个度量值是为了赋予“其他品牌”最大销量值。

这里用到了一个小技巧，我们要把所有排名在N+1之后的品牌全部赋予一个固定排名数字：0，然后在筛选器里屏蔽这个排名为0的品牌，这样就成功实现了我们的目标。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFzKhocNdoiaqdxic0MTicqkbu0rULYa9LcDibAAxS1B3bpgSBCViaQORmVZQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**问题2：如何让其他品牌显示正确的销量？**

这个就简单啦，还是利用我们刚刚建立的\[销量（含其他品牌）\]度量值，只要把刚刚设置的数字3替换成参数N即可。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFBHkCZzIXEg1hsaFmHQKudGjnaZX3qq3cNdYkSR8Qq6lAyjHwp5OdXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

我们来看一看效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFLUTyCUCVqkjGoBomWF37ZyFQ7EuAyaDBelEdQ2ugLDSnmJlReId9kg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

至此，还有一个细节问题，现在的图例默认是按照销量大小排序的，如果我想让“其他品牌”永远排序最后一位，该如何实现呢？

很简单，还是利用度量值，我们新建一个度量值叫做\[品牌排序参照\]:

> 品牌排序参照 = 
> 
> IF(SELECTEDVALUE('全品牌数据'\[品牌\]) = "其他品牌", 
> 
>     0, \[销量(含其他品牌)\])

然后将这个度量值拖到工具提示，选择排序方式按照\[品牌排序参照\]排序。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFqlq46OqFib1ZzoSt2KIK5jKzLdC6fgnf3peFbGndh8l0Wia7g0vCSmKA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

  

最终效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOHT70bTG69tHlibYLCRibwlFw5CKsKLibLZrqB8UXB2CM4N7mXfyiaLfdTn7Z7toJ24SgicUJgIPhAqwA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

好啦，目标达成，现在你也可以动手试试，能否帮助你解决一些类似的日常业务场景吧！ 

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.4k+ 学习者一起成长
