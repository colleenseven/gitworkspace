---
create_date: 2022-03-26T11:57:21 (UTC +08:00)
tags: 
pagetitle: Power BI报告中的动画效果，利用这三种方式轻松实现
source: https://mp.weixin.qq.com/s/dHFEFQ_4wjiWX1CYopuPAQ
author: 采悟
status: 未阅读
category: 
uid: 
---

PowerBI做设计报告时，不仅可以调整各种元素的色彩，还可以在某些地方插入图片作为背景来丰富效果，经常有人问能不能在PowerBI中插入动画，其实gif动画也是一种图片，一般来说，只要能使用图片的地方，就可以使用gif图片制作动画效果。

但是如果直接通过PowerBI功能栏上插入>图像，如下图。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhElRMwXLTbuhaG6mb2iaa3gcRupXjD1qCX1TsYqOBuEmjQo4Tjc8zzGLXg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

即使你选择插入的是gif图片，也没有动态效果的，而是静止的状态，也就无法直接使用这个功能来实现动画效果。

虽然直接插入图片不行，不过还有几个地方是可以实现动画效果的，本文介绍一下，利用内置的可视化元素插入动画的几种方法和场景。  

**1、在图表背景中插入动画**

这是一个常见的柱形图：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhEluupXYRtEz8WajgJuPjicnaiau8mVAC6xialsjiaF3NCxESbFKYub2H9XIw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

打开图表的格式面板，在里面找到“绘图区背景”：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhElasIrMQ1QuuvOuLPaJAxaBgt4spm39Cvde77Wcvwswa0qdiaH2sUqqjA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

点击进入，浏览电脑中保存的gif图片：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhElJIIU9jb8YpicKGxDMibBPMuicxcXl2tcltx2gel7Bq881cicapQI0seI6Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后就可以得到一个动画背景的柱形图：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhElBZZoFtBh01giaYDCKOPUicia59icS7jFgyx1OOPxZib07jialADeLp0SZibfQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

PowerBI内置的柱形图、折线图、瀑布图、散点图等，都有“绘图区背景”的设置，也就都可以设置图片动画的效果，如果你使用的某个图表，没有看到这个设置选项，那么就是该图表不支持。  

**2、在按钮插入动画**

按钮经常与书签结合，用来设计报表的个性化交互。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhElIXTg99aOuJJMrxKKUOeaKRtlNBILhtsVZ9BGA0wNGDgkNIe9ic15bTg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

在PowerBI中，还可以利用按钮来插入动画效果，比如插入一个空白按钮，然后在按钮的格式面板中，找到样式>填充，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhEl3cJQwvicnAGbjaAMWVicPJwuObGxUgJpWoLibWZKOc6Js0lKluBbZJ1JA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后选择gif图片就可以了。

下面左图是默认的按钮，右图是带动画的按钮效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhElZ9Yur1G2zKv5hY5bQRIASKw11SpRvh6Vz5WpmRIDlgIHxoFTp0BCuw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

按钮上添加文本，就可以做成类似下面的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhEleNL374VeZpdnbiajVRzmRSquSVdc9CDRh8QrYHQPmx1nicwAQRJtQtbg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

其实利用按钮，不是只能做这种简单的图标来做按钮，只要是gif图片都可以的，根据你的需要可以随意插入动图，比如下面这个做成报告标题的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJM8HkrGU9nGD1fNWfP3jhElhetIY1FLUlQlj1TXzeyVny0ictibjMktiabm72qBicoqmaV9KTuPd1swew/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

利用按钮来设计动画效果非常灵活，把它当成普通的插入图像的功能就可以啦。

**3、在页面背景中插入动图**

这个是最经常用到的，可以用于丰富报告的首页，页面背景动画效果如下：

（你喜欢哪一款呢，欢迎点赞留言）  

关于这种做法，之前曾经写过方法，请参考：[如何为Power BI报表设计动画背景？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074267&idx=1&sn=144af32ea82f858fabf8278f3ba1d50f&chksm=8e0c5dccb97bd4daff38ffd25857e1d5137fc6ecb77483f764c3ba04740dddd348ef5359f12e&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074267&idx=1&sn=144af32ea82f858fabf8278f3ba1d50f&chksm=8e0c5dccb97bd4daff38ffd25857e1d5137fc6ecb77483f764c3ba04740dddd348ef5359f12e&scene=21#wechat_redirect)

这里就不再重复介绍了。  

关于动画效果的设计，方法很简单，关键是灵活运用，平时多收集相关素材，本文用到的这几个gif图片，可以在PowerBI星球公众号对话框发送“**gif图片**”获取。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
