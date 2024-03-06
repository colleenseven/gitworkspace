---
create_date: 2021-01-21T20:20:50 (UTC +08:00)
tags:
aliases:
pagetitle: Excel中PowerQuery的全自动动态路径
source: https://mp.weixin.qq.com/s/lW2IzVMaR9hxvK-mgeKZ9Q
author: 采悟
status: 已完成
category: 浏览文章 
notes: false
ZK: Origin
uid:
---

关于PowerQuery获取数据的路径，之前分享过利用参数动态化的文章，参考：[PowerQuery报错？利用参数轻松解决源文件路径问题](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073358&idx=1&sn=99e86bdde3a9831509fc8017890e0af8&chksm=8e0c5959b97bd04f4023fe469acc7774bf8307856086b58133d10b61bf518970b4fa7fbbdfe7&scene=21#wechat_redirect)

这种做法并不是一劳永逸的，路径变更以后，还是需要手动调整路径参数，只是相对方便一些而已。

在PowerBI中目前只能按照上述方式实现，但是如果是在Excel中利用PowerQuery来清洗数据，是可以做到自动更改路径地址的。

假设是从单一的文件中获取数据，以数据源文件为Excel工作簿为例，PowerQuery中【源】的代码是这样的：

> \= Excel.Workbook(File.Contents(**"D:\\PowerBI星球\\PowerQuery动态路径\\示例数据.xlsx"**), null, true)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOicfq9iaeIsO8d8urU9icX5NOR069fnvu8VuqvDfZRCMFOibRK9aZlEj8pYDeSYYwH0VTpyRaovt5xbQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

现在要做的就是将这串代码中的路径文本动态化，方法很简单，只需要用Excel公式将当前的路径提取出来。

在PowerQuery查询所在的Excel工作簿中新建一个sheet，A2中录入文件名称，B2中输入公式：

> \=LEFT(CELL("filename"),FIND("\[",CELL("filename"))-1)&A2

做成这样的一个表：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOicfq9iaeIsO8d8urU9icX5NOKg5rVS4LSic1RKj16Cauud7dD9gwx5AsuKjDuudQDIMwY0La3DYGogA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后光标放到这个表的任意位置，在【数据】选项卡下，点击“来自表/区域”，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOicfq9iaeIsO8d8urU9icX5NOiaoNWckdwgtUYrVdViaGDjUCicIrbS3jyqk0zv7JYX2xHBhyp0MMVEWTA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将这个表导入到PowerQuery编辑器中，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOicfq9iaeIsO8d8urU9icX5NOGF2l0yvRAFYmHP4EjNnnF1J3I1yusM2mBbNcMSNaicJzmYQItmfHXOQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就得到了文件路径表，第1行路径列的数据可以用  **文件路径{0}\[路径\]**  表示，只需要将原查询中路径地址更改为这个代码就行了，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOicfq9iaeIsO8d8urU9icX5NOFlY4eWCcnmzWpAleeETAINRtPFQsKqTN7axRkUR8awm3o6kjsibzvxQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

修改完参数后，可能会出现如下报错信息：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6YhFYHymUSdNvTgicIguRHUz24lgA6rkwutWxPLZpquxhBicLQNvaibbHUsoF5w5bGYXQhuIgUK3xw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种情况需要在文件>选项和设置>查询选项>隐私中，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6YhFYHymUSdNvTgicIguRHrAYHVjoFX4mXuWoUMRt2uKBiciamcA2EMT7RHXTsexwt4PNJKRvnspUA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将隐藏级别更改为“始终忽略隐私级别设置”

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6YhFYHymUSdNvTgicIguRHq8DQIPqzpv34QrNkpER3FQrohPKYpBib19T77VHBKOIa5icZ6WnCd35A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击刷新即可。

如果源文件是文件夹，同样可以利用这种方法，先获取文件夹的地址：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOicfq9iaeIsO8d8urU9icX5NOvBohOGxm79sFpricvW8LCCakXoiao6VaCoq2E9CZWMuzYNABeKdM8qQQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

按上述方式导入到PQ后，然后将获取文件夹数据的查询【源】代码中的路径更改为文件夹的路径即可：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOicfq9iaeIsO8d8urU9icX5NOHy1Xl97mahniaET41iar1tsWgPSurGz4eeRla2QcoJphRibjNZcZQsrJQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样处理以后，无论将文件移动到哪里，还是发给别人，都不用调整代码、直接刷新而不会出错。

**该方法的关键是必须将PowerQuery查询所在的工作簿与源文件放到同一个路径下，这样获取本文件的路径，同时也就是源文件的路径。**  

最后说明一下，本文的方法仅适用于Excel，不适用于PowerBI，为什么强大的PowerBI反而没有这个功能呢？

其实很简单，因为在PowerBI中，还没有函数获取本文件的路径地址，而Excel通过cell函数就可以实现，上述方面正是利用了Excel的这个特性，实现了PowerQuery源数据路径的自动调整。

