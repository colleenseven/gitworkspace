---
create_date: 2020-09-29T20:35:51 (UTC +08:00)
tags:
aliases:
pagetitle: PowerQuery报错？利用参数轻松解决源文件路径问题
source: https://mp.weixin.qq.com/s/3y5qVX-Xn5_dF13b8WkC9g
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

PowerBI可以很方便的从Excel等文件中获取数据，但这个路径是绝对地址，如果源文件路径发生变动，在PowerBI中就无法刷新了，并且进入PowerQuery编辑器中也会报错，看不到数据处理步骤。

比如，原来的源文件路径在C盘，如果你把这个源文件移到了D盘，再打开PowerQuery编辑器，你会看到这个界面：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMkuQIica4M0eNx7Iy2WzVqYcnRCbGmOmV5vqbgfKRiaTG8TSHDRp5wFMvA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看到这个界面是不是熟悉而无奈。

这种情况更多的场景，可能并不是自己的源文件变动了，而是收到别人发来的pbix文件以及Excel数据源文件，你把Excel文件保存的地址与对方在pbix中设置的不同，导致无法刷新。

解决的办法就是手动直接更改源文件地址，有下面几种方式：

**1，修改步骤【源】，重新选择文件路径。**

点击【源】旁边的小齿轮按钮，即可在弹出的窗口中浏览路径，选择数据源文件所在的新路径即可。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMk8UQ1ssCUpEOJbmiaDialetMe3KvKEcUL7c3N31jtPabdvkoQT0xMsTLA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2，在编辑栏直接修改路径地址。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMksyf9zibiaiaIVNlc7sZhjibGvcwEcCKdyGOpT6oC6ia0ZL9gA9zKy8UsKwA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3，打开高级编辑器修改路径地址。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMkMNkrg7qR0aoWuJ70rlofwznUoWKpU5rDOyEglv6SWVkrqrgW8ic9QvA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面几种方式，都可以很简单的解决这个问题，不过如果表比较多，需要一个个单独修改，比如上面的数据，有5个表，那么就需要修改5次。

  
并且，如果接收文件的人对PowerQuery、PowerBI不熟悉，甚至无法独立完成修改工作。

**有没有更简便的办法呢？下面才是本文介绍的重点，利用PowerQuery中的参数来快速修改路径地址。**

具体操作步骤如下：  

**一、新建参数**

在PowerQuery编辑器中，点击管理参数>新建参数：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMkWVBxB8R5BviaicjR1d1FKeicAlXvdjbTwOxMVTv8b3GIOqYuPlE932b3g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

输入参数的名称，类型可以选择任意，当前值输入源文件的路径地址。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMkc8vDAUIP3s7LylX0f80FQ3s3jXAT2c2ic3Siacw06gSz9UCo6iaiaT3ZXg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后这个参数就建好了。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMkbWZ3JzXDXjGCt2RHiarx5BmYbhLLJp9jz1f8nLmXNXpBp2icxDsgfmEQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**二、将代码中的绝对路径地址修改为参数名称。**

与上面的直接修改路径地址一样，可以在编辑栏或者高级编辑器中，将绝对地址修改为新建的参数名称，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMkc0ENlaHYPVxNqKSlRKbosuicHrcgAWiabJg1ibVezBibruJVerdsw25dZg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**注意原来的绝对路径地址需要加双引号，改成参数后不需要再加引号。**  

每个表都这样修改之后，如果源文件路径发生变动，或者你保存的源文件地址与pbix文件不一致时，只需要修改这个参数值即可。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMkUmIzdQxPGXTM0eDA73qicswIDOibtQr8JZhibOUd3pnQ3TibK85O8ck0UQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后PQ中所有表的地址就可以一次性的变更过来。  

**如果有确定的几个可能存储地址，还可以构建参数列表**，在【建议的值】选择“值列表”，并在下面的表格中输入几个路径地址：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1C5Nmac8unDajK4DibGAMkVgQuqHJszHbpv5PbxgcrickwDhuW8FN4OZGC61LT3wn9dkNj3GFKbHA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

比如把每个盘的路径都数据进去，这样无论将源文件存放在哪个路径，直接在下拉框中选择就行了，手动输入都省去了：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO1C5Nmac8unDajK4DibGAMkOCJ0GVr4fVbTEEiaN71RMkzl9dGROhVWytlzGZEldrfaDiafFSPxn2xA/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样是不是就方便多了。  

下次你也尝试用这种方法来管理源文件路径，这样当你把文件发给其他人时，即使他对PQ完全不熟悉，也可以利用界面式的操作，快速切换本地的存储路径，而无需接触到“高深的”M代码。

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072121&idx=1&sn=4b6b96811e263c4079f606cfab14976f&chksm=8e0c446eb97bcd7876ffa2d5bb5feae5c175353d1e957b72ae3732ad67c89a6f9f42c61af833&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMst6LMfyIX5sg2QmEtLfjxR5h1x8nrN7ibw97H9HjLSB59iaf2JLMtwY8OUcKiacK35ybYfpaoVNuGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071399&idx=1&sn=44b4ba20c1cbe657f77b6c8d144b2b30&chksm=8e0c4130b97bc826d87746723f940404ce82ac9ebb38572bbfb1a89d7a48aaa750dffd92a28d&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtHORfNDsk1ibQ1luXtyibbDsnnwJXvdSpKwfPlcJCZSlvWYOK6p6VGeqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070526&idx=1&sn=fd4131317654df2ee7619cfc58e2987c&chksm=8e0c42a9b97bcbbff556f8cb013259a7981c0847d4ea656d63af3a438af3aa33a38974d7145a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

↑ 扫码加入，和2.4k+ 学习者一起成长
