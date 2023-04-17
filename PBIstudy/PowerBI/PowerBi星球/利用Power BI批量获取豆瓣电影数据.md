---
create_date: 2020-10-05T20:34:02 (UTC +08:00)
tags:
aliases:
pagetitle: 利用Power BI批量获取豆瓣电影数据
source: https://mp.weixin.qq.com/s/t9v6gVSR5YhhygpCAZeytQ
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

2020年的电影市场沉寂了大半年，随着国庆档几部影片的上映，差不多恢复到了往年的热度，不过打算看哪部电影不能仅看是否热门，更靠谱的是参考电影评分，更准确的说，是看豆瓣的评分。  

这篇文章就来看看如何用PowerBI批量抓取豆瓣电影的数据。以最近正在上映的电影为例，豆瓣网址为：

https://movie.douban.com/

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawESF4htg04iadprs2J3DgsNAoMJcfBkibGN9QdzicGmwAtmia1ic9R6Kib1P1A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

利用从web获取数据的功能，将这个网址放进去，就可以轻松获取这些影片的评分：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawE3FaUhSTicQUEk0K8Vzzicm1R1poqDyTZLTyEXHN0KgSaBPKrtUiaUlLXg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种方式抓取的只有一个评分数据，其实在每部电影的详情页，有更丰富的数据，比如电影的导演、主演、评分人数、影评条数等。

比如最近最热门的电影《姜子牙》的豆瓣详情页：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEhwCic2tUe4FtT3DjV8VuibUqQhVIPx5rzUAaplUSbaGEeEtKg2fQ03bA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如何能批量抓取每一部电影详情页中的这些数据呢？下面就来看看操作步骤。

**1、批量获取电影的详情页网址。**

要想获得详情页的数据，首先就需要先得到每部电影的详情页网址，批量获取网址的方法，之前也介绍过（参考：[Power BI如何获取网页中的链接？这个方法非常好用](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070458&idx=1&sn=c4c2f4de681ef66524b91209e83dd769&chksm=8e0c42edb97bcbfb525a923d9d7378095f91ae9e3d592e28b7918ee1ea8a991b49ed4017fee0&scene=21#wechat_redirect)）。

先打开前两部电影的详情页并将网址复制下来，然后利用"使用示例添加表"的功能，将前两行数据粘贴到前两行，系统就可以自动识别并补全剩余的信息。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEOicF0r36n1z3lrFRavefnsvlPTDiaGE87TFz2iaD8eamzMic5etNZYyB0w/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

或许是豆瓣电影网页的数据结构不够规范，所以提取出来的数据，与网站实际看到的略有出入，将重复的、以及不正确的数据删除即可。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEcTVN8Rqz6hGzGYZ8KfvQMt7Urf1y0nUglRF6k77kIvHdx6lkl3NGrw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2、提取某一部电影详情页需要的数据。**

选择某一个电影，进入详情页，比如提取出《姜子牙》的导演、主演、评分人数等数据，依然"使用示例添加表"，将这些数据提取成一行，

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEnXd36KWN2iaLZJpIpLiczC61zbZGmDB5gKQ6F4F6ndu63iccHBLbQpt5A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

然后将这一行数据清洗成规范的数据。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEzOaUBiaGwV1WOcYnFCTzw11bYMsmbmqYSXaBC0kYHusG0IPVicBPH1LQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3、利用第2步的查询建立自定义函数。**

右键该查询>创建函数，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawE9v3mtSueibxGeyEjk4Ry3rvnkkic2l71Nr8J4Nibu3wTLwhlfNiaH3u1eg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

命名为movieinfo，并修改前两行代码，定义网址为参数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawElMASduUJGJkVhSZ1dEuILmem3slROLaCOMP27StImrVeqNHWIZBakw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

自定义函数制作完成。

**4、调用自定义函数。**

在第1步查询的基础上，调用创建好的自定义函数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEMWw1DSlUukQ7eOBC0aqxO5qyMbvOVl3hLCRHQaHaQgwiazNh8vibGzzw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后展开数据即可获得每一部电影的详细数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawEAN0mUic8VZfg9ibEfg96ibTHe8eT7CBkrwPicoQiblBoQib4iaIdEmP22jn0Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将抓取到的数据上载到数据模型中就可以进行分析了，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOALjJDFtKIibG8jZFGoeawESWBFJJu2RlOwxVjFVfrVemGOK1Mx959xRuOItJrQ9U0qQjR3UFghwQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

不得不说，之前备受瞩目的《花木兰》评分真的好低，不推荐观看。  

以上就是PowerBI批量抓取链接网页中数据的步骤，具体细节，可能不同的网站需要不同的处理，但整体思路基本如此。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.5k+ 学习者一起成长
