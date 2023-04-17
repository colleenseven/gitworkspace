---
create_date: 2020-10-31T20:28:37 (UTC +08:00)
tags:
aliases:
pagetitle: 利用PowerBI的这个控件，美化你的切片器
source: https://mp.weixin.qq.com/s/NPOR0geStggip30e2S1Knw
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

## 切片器是报表设计的一个最常用也是最重要的控件，很多动态的交互都依靠切片器来完成，它的功能和用法也很简单，上手即用，PowerBI中内置的切片器几乎都能实现大多数所需要的效果。

但是内置切片器的自定义设置有限，很多人想设计个性化的效果，就不容易做到，今天就推荐另外一个切片器：Chiclet Slicer。

其实之前文章的示例报告中，很多切片器都是用的Chiclet Slicer，比如[财务报表分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)的示例中，切片器有鼠标悬停的效果，就用用Chiclet Slicer实现的。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOomn9seglicbYJWoORuuBJxQ8QqQaITSsT3ibMzphUYp1Vufw1ImdNCjCeQPTK7TMvrtxCE1D51X8A/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

下面就简单介绍一下Chiclet Slicer的用法和主要功能。

首先在AppSource中加载这个自定义视觉对象：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxMFciblBGoXcjEfZ3l7Fy56ia91d2ARh3SicKqEMMGDKX92y5tl3vKRA5A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 搜索的时候，记得先在分类中选择“全部”，然后才能搜索到哦。

Chiclet Slicer是一个按钮式切片器，默认的效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxmaluONBiceJIwJP7D6z6Xk8xbAday6LKhptnMktLsIfQp6TZKCt34iaQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

可以在格式面板>常规中设置排列的方向、每行每列的个数以及是否强制单选等，这些和默认切片器的功能差不多，下面主要介绍几个默认切片器没有的功能。

**批量多选**

正常情况下，按住Ctrl键可以多选，不过每个选线都要单独点中才能选取。而在Chiclet Slicer，按住Alt键，点击头尾两个选项，中间的都会同时选中。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOomn9seglicbYJWoORuuBJxgic6ndZllh0htYQBjWdtpyziaGK6j2y7FU5LOvvIgsD7s1a8XPb4z8Jg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**自定义选中、悬停颜色**

在格式设置中，有丰富的切片器元素自定义选项：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJOomn9seglicbYJWoORuuBJxJib8PN16jOtia1FribL1bEveH5p8kITPt05bGvUoVfWPWB2wJicTnib0ticA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

利用这些选项，可以轻松设置成这样：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxzdZc6k62bofJtuTia6JWAqwHVbALqouwjP3ibYDyQGDG5jcqyEsicicUHg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**图片支持**

这是最好用的一个功能，可以将图片填充到切片器上。假如报表中有个品牌切片器，正常情况下，切片器是这样的：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxnOiaaeIbcAD7wK7ru3Nv47zlbmfVVicYpydl7Brajfts3oCleia8lSTOg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

为了更加直观，可以将把每个品牌的logo放上去，步骤如下：  

**1，找到logo图标，并发到网页上生成一个网址，将网址添加到品牌表中：**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxBl9b5qibmYU01jCnaTKJ97oI7NucgyUiae4lIY3SP1Qz7Z1PF96ylcpw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2，设置字段\[logo\]的类型为“图像URL”，**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxiasKkcvicg1jec02tjgRlfuJVZibgdKLWcIibOV5cDEGC6icw8eB0dxa8cQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3，将这个logo字段放到Chiclet Slicer的【图像】框中，**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxYofkLTiauGe6ql0GbM4DLCCxJ5TBdMymxB3FupHVt0xmz3oIjGibRtAg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就生成一个带有logo的切片器了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxJn6Tfn6WhsYAEvhCibZic19neNeVhFia2aV8bicYge3fANfHN5vY2zJkNA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 还可以继续美化，文字都不要显示了，只用logo来筛选：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOomn9seglicbYJWoORuuBJxNXIUdvGpUSjibPvXrTqexzVaBKMZDIcTf43u3l07JwUW1ORmG07q5VA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

## 是不是很有趣。  

Chiclet Slicer是一个很出色的控件，下次再设计报告时，你也可以尝试一下它的效果。

如果你无法下载该控件，可以在公众号对话框发送“ChicletSlicer”获取安装文件。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.6k+ 学习者一起成长
