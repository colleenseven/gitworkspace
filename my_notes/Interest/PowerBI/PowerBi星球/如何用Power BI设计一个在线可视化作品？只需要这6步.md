---
create_date: 2021-10-05T22:40:26 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何用Power BI设计一个在线可视化作品？只需要这6步
source: https://mp.weixin.qq.com/s/bm4N9IAs9crW0JLWTUo3uA
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

如何用Power BI制作一个在线可视化作品？  

这个问题可能很多初学者都想知道，第一次接触PowerBI时，也许就是因为看到别人分享的一个PowerBI报告的网页链接，打开竟然还能点击交互，惊为天人，然后投入PowerBI的怀抱，期望自己也能很快学会做一个这样的动态报告。

**但是真正开始学习Power BI，天天接触的却是枯燥的PowerQuery、DAX等知识，学了好长时间，却发现要学的东西越来越多，距离做一个可视化报告越来越遥远，仿佛入了一个大坑，你是不是有这种感觉呢？**

在PowerBI中，M、DAX等这些技术确实是难点，这是为了处理不够规范的数据结构、复杂的分析需求而必须掌握的，但如果你只是想做一个简易的可视化报告，其实真的不难，甚至不需要学习任何公式，只需要简单的几个步骤就可以做到。

以现在国庆假期热映的电影为例，如何做一个在线自动更新的票房排行榜呢？这个需求用PowerBI非常简单，任何人、用免费的账户，就可以零成本的做出一个在线定时刷新的报告，我做了一个效果如下：

你也可以点击本文底部的“**阅读原文**”，查看在线报告，文章最后也分享该报告的源文件。

下面就将这个报告拆解为6个步骤，让你看看PowerBI是如何做出来的？

**1\. 获取数据**

第一步是获取数据，如果是自己的本地数据，直接导入到PowerBI中就可以了，然后根据需要整理，这个步骤非常简单。  

这个报告数据是动态变化的电影票房，所以用了PowerQuery来抓取网页信息，这里用了艺恩数据，网址为：

https://www.endata.com.cn/BoxOffice/index.html

关于从网页中抓取数据和图片比较简单，具体步骤不再详细介绍，可以参考这两篇文章：

[数据获取，PQ就是这么任性！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067131&idx=1&sn=cac2f0f5b79169cbba61bf207bee1532&chksm=8e0c71ecb97bf8fa211533583fcf92f374a96d3eba85c1cffabbac3639d40335fbd188761f7d&scene=21#wechat_redirect)  

[Power BI如何获取网页中的链接？这个方法非常好用](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070458&idx=1&sn=c4c2f4de681ef66524b91209e83dd769&chksm=8e0c42edb97bcbfb525a923d9d7378095f91ae9e3d592e28b7918ee1ea8a991b49ed4017fee0&scene=21#wechat_redirect)  

从网页中抓取了这两个数据表：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZtHWyM6GnewAoeAWC3Qy2XTykRtjKswB8SPnlBsKwQpgWIPURIjFf8PQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZt3xmZPKgo0e4hsqUOnKwATczKdPVUlHEQUdC2FXBdtRCosfvuRErt6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. 数据建模**

只需要把上面两个表建立个关系就行了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZt2NDdX4gQfh2GgibCZQ372B9pnW4qlwtA3icOFpqYvk3eIicB62RJ2icEgA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里用的是电影名称字段，建立的一对一双向关系，这样的关系其实就相当于一个表，而不需要专门将两个表合并成一个表。

因为这里的数据非常简单，所以这里就不单独介绍了，如果你的数据涉及多个表，需要建立数据模型，可以参考：[Power BI数据建模](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067199&idx=1&sn=3392bb969a2432d09bdc5af39972d8ce&chksm=8e0c71a8b97bf8be1503fe66a62b49fdec34bfa953f55c575b24308440fc5286ba9ef15c04ed&scene=21#wechat_redirect)

关于PowerBI的学习，可能主要精力会放在一块，它也是难度最高的，但是如果你的数据很规范，需求也比较简单，其实也并没有那么难。  

**3\. 制作图表**

数据整理并建立好合适的模型以后，就可以进行数据可视化了。  

这个报告的主体只是一个表格，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZtk1C9blPoW2UF1XZOQdhgRQhosGqCHCPtFqypU5fian6mlIUjDiatHozA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

为了展示每个影片的详细信息，单独做了一个页面作为工具提示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZtiaC9WzSzmMYnQByVWT1E8tR0JunSpkZhCO5wMe7AzHurnuNWQRzv9LQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于工具提示的制作，请参考：[深入了解PowerBI的工具提示功能](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067562&idx=1&sn=c3472d97c251abf52f38e2f7e31b23a6&chksm=8e0c763db97bff2bf8d514625a3fd037d274ea3014624766b7aa2822bc63a6e2c96006223ba7&scene=21#wechat_redirect)

**4\. 报告设计**

为了让可视化报表更像一个报告，而不是几个图表堆放在一起，可以调整报告的尺寸、添加背景图片等设计元素，它们是在格式中设置的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZtFBsxnckt4sibY6JCqfVgTxIVQ8rDmjpYugQFpNZeYR88JpxpfsibwTGg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

背景图片可以先在PPT中设计好，导出为图片，然后添加到PowerBI报告的页面背景。

因为现在PowerBI中的设计元素，相比PPT还差很远，所以包括标题都可以在PPT中做好，只留出放置图表的区域就可以了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZt0ficcfEIstVHay7mUG3vJWhrZIVxyiadGMpUibMfslLyodPy7g6DJSFXg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里只是一个页面，设计很简单，当报告较大、页面较多时，还会涉及到报告的布局和导航等技巧，也可以参考这篇文章：

[Power BI财务报表分析：报告设计篇](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

**5\. 在线分享**

为了方便分享给他人，需要将本地报告发布到PowerBI服务中，先在Desktop中点击发布按钮：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZtaNoscKfCpCXtjqkQa3O1rIBBnHv4QicOHPqrdfp6c9NzfXWdZhVMKwg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就将这个报告发布到云端了。

当然发布前必须先登录，也就是必须有自己的账户，如果你还不知道怎么注册账户，可以参考这篇文章：[超级秘籍：免费拥有可发布的Power BI账户](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070700&idx=1&sn=7b97e421ea46cbfacca3f6aed4ef1720&chksm=8e0c43fbb97bcaed90c9d5b835de96be15e16e7944c5cf075a98232b41b3236f3ab95dd38d20&scene=21#wechat_redirect)

**上面的步骤，都是在PowerBI Desktop中完成的，为了便于他人查看最新的报告，下面的步骤需要进入到PowerBI 服务。**

国内账户登录网址为：app.powerbi.cn

国际账户登录网址为：app.powerbi.com

登录到PowerBI服务后，在工作区中，会看到两个文件：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZtuf80nDPrIamJqeyn1ticMMSeicc7Pibia0TwDibMgU4aSHSUzeSBp4iatNxg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上面的是报表，下面的是数据集，先打开报表，如果是可以公开发布的报告，比如这个示例，就可以发布到web：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZtGXoyA7bKRqKZhWo5yPsftlSfvPUMw93Oc6x5ZjBX4HdSpa4r5dnuuA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就会生成一个网址，把这个网址分享给他人，对方就可以直接打开查看，并且可以点击交互。  

发布到web这种方式，适合可以公开的数据，如果是内部敏感数据，不要使用这种方式，可以购买Pro账户，按角色权限分享，保护数据安全，参考：

[利用Power BI行级安全性，限制用户访问权限](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076638&idx=1&sn=04e90c833a99f5a0e9b2baa06b5c4a8e&chksm=8e13aa89b964239f010a579a4bfdb74ce2dd483b7d333d4a797ca03c12752ab75c1a0fa4e05e&scene=21#wechat_redirect)  

**6\. 设置刷新计划**

通过上面的步骤，其实已经实现了在线的可视化报告，如果你的数据需要定时刷新，还可以在PowerBI服务中设置刷新计划，具体操作步骤可以参考这篇文章：

[**利用网关实现Power BI报告的自动刷新**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076890&idx=1&sn=d50a0875dccb56423464b2af3742bd36&chksm=8e13ab8db964229bfc354e4039f72370bfe6cde7b43fd87dc11062a8bcd72cf35e7f2cc44cc4&scene=21#wechat_redirect)

然后这个PowerBI报告就会自动按计划刷新，再打开在线网址，就会自动为动态刷新后的数据。

以上就是一个自动刷新的PowerBI在线可视化报告的制作步骤，没有用到复杂的DAX公式，基本都是界面操作，并没有难度。

这里有意用了一个非常简单的数据，完成一个可视化作品，目的就是让你直观的看到，PowerBI从原始数据到最终的可视化报告作品的全部流程，而不至于迷失到某个模块的学习中，学了很久也不知道PowerBI到底有什么用、怎么用。

**你也可以尝试着从简单的数据开始，制作可视化报告作品，当你做出一个PowerBI报告，并获得你的领导或者客户的赞许时，你会有满满的成就感，然后学习起来也会更加有动力。**

并且你先做出一个简单的可视化作品，对整个流程有了更清晰的思路，如果日常面对的是更复杂的数据和分析需求，就针对性的去学习相应的模块，补充相关知识技能，这种主动性的学习不会让你感到枯燥，因为你能感觉到，你是在掌握某个环节的知识，它可以帮你不断完善最终的作品。  

**这就是以始为终、产品思维，对于学习PowerBI同样有用。**

上面的操作步骤，由于篇幅有限以及避免纠缠到细节中，让你更加困惑认不清方向，所以我并没有介绍所有的细节，如果你练习时遇到问题，可以参考**这个报告的源文件，****在PowerBI星球公众号后台发送"国庆电影票房"获取。**

___

最后，PowerBI星球学习社群内容升级，增加视频课程，**涨价倒计时，现在还可以享受国庆专属优惠券，数量有限**，如果你感兴趣，不要错过：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO9TfUv7UNicOYAzns4P2mZtrCoE2JWeNJ92ZibWv2MnPBLhADmHPrkZMx2mrIOXpHiaABodQAg4Rupw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

 **常见疑问解答：**

**知识星球只能在手机上使用吗？**

知识星球除了手机APP，还有知识星球网页版，PC端登录 wx.zsxq.com，即可进入知识星球网页版浏览、提问、下载。

**付费有效期是多久？**

会员费为年费，自加入当天开始有效期365天，会员续费时可享超低折扣。

**注：****到期日之前星球中已发布的所有内容都可以永久查看**。

**如果你对PowerBI星球社群还有什么疑问，可以添加采悟微信（powerbi001）咨询。**

采悟微信号，欢迎交流
