---
create_date: 2022-06-12T12:33:00 (UTC +08:00)
tags: 
pagetitle: 利用Power BI的书签导航器，原来设计导航如此简单
source: https://mp.weixin.qq.com/s/2ejylP6j-REoMhUw806e0Q
author: 采悟
status: 未阅读
category: 
uid: 
---

前面的文章介绍了[页面导航器](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080516&idx=1&sn=0290f2762815188f0b96e03f3f25fe7b&chksm=8e13a553b9642c45ecf32e51e95720e7f82a4ec9691bc00b6aaee95f12fd30e312557f5ce381&scene=21#wechat_redirect)，和它同时发布的功能中，还有一个也同样有用，它就是**书签导航器**。

关于导航的设计，并不仅仅是针对页面的导航，比页面导航更灵活的是利用书签导航，即使只有一个页面，也可以利用书签设计灵活的切换效果，比如之前介绍的[页内导航](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080023&idx=1&sn=001ead7e1723917c204db70d6f198425&chksm=8e13a740b9642e5620efbd3bfecfc47c3b33062715dc6d5e48f033010fb815a07ee090c8fb52&scene=21#wechat_redirect)：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2dk7iagThG1NwU65N3uiaCvqlzwXoCJ6oSWlibPOuuabqJ2X49O9TDeIPQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这种效果是在一个页面内的切换，无法使用页面导航器，之前是利用书签实现的，这里改用书签导航器来制作并带你熟悉它的用法。

以这个[页内导航](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080023&idx=1&sn=001ead7e1723917c204db70d6f198425&chksm=8e13a740b9642e5620efbd3bfecfc47c3b33062715dc6d5e48f033010fb815a07ee090c8fb52&scene=21#wechat_redirect)的效果为例，首先制作好三个书签（这里的书签只需要包含几个图表就行了，不再需要插入按钮，也不再需要页面背景图片中放入按钮），直接在“插入”选项卡上点击“按钮”，选择导航器>书签导航器：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcrakssTXuLhicuxOb5m24EGsVl3OCAem7lFTLKIQv8xnRdeTiaPJYTb1qoA4ZzFLp6SIXyolWP4A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后自动就会添加一组按钮组成的导航器：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcrakssTXuLhicuxOb5m24zx0zqmEMNaItmnxqwmdolXoWayP8k1jPybBuuwvbSlMXrWrXtVDhAw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就可以像普通的按钮一样点击切换书签了，是不是非常方便！

书签导航器中的这组按钮也会随着报表书签的变动而自动同步，特点如下：

-   按钮的标题与书签显示名称一致
    
-   按钮的顺序与报表书签的顺序一致
    
-   所选按钮是最后一个选中的书签
    
-   在报表中添加或删除书签时，导航器会自动更新
    
-   重命名书签时，按钮的标题会自动更新
    

如果对默认的效果不满意，你还可以选中生成的书签导航器，然后在设置面板上，对按钮的形状、样式、布局等各项元素进行自定义调整：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcrakssTXuLhicuxOb5m240Nemh83xBVcUc5e6WuRTTUPkhvYHY12wpvMlzC25RRGnaC3SbumxGQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

比如将形状更改为“药丸”：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcrakssTXuLhicuxOb5m24QUqEc2GUZcFgK6WfSujYBicG5ZU7MPZMY3DaG6vQ0pCaDiaG9ocRUoUA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

使用页面导航器时，会遇到某些页面不需要放入导航器的问题，通过一定的设置就可以解决；在书签导航器中，同样会有这样的问题。

一个报告中可能有很多书签，但是制作某个书签导航器时，只需要其中一部分书签，比如之前介绍的[局部切换](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080041&idx=1&sn=1e9699099902ed7dded7c60f65661585&chksm=8e13a77eb9642e68c3922d958fe66c52f3ba0f1a35954fbef7309c0ee4b33801ca7eb53ab54c&scene=21#wechat_redirect)，效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMOw9BKOEkR7xE1eRLoPOibBMtHJnOTsht13vTIHVHRXj4Kg26QDqwoibGwpbTl3CNIRtJPy8Yx6XhQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

上面是一组书签，下面是另一组书签，如果直接插入书签导航器，默认的导航器中会出现所有的书签：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcrakssTXuLhicuxOb5m24chibNCOz72N5uczghXUuxzcGdLicjMmwHGticibBrhky0ttjet19XOo0Hg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这明显不符合我们的需要，**其实这页报告中需要建两个书签导航器，每个导航器只包含部分书签，这种应该如何用书签导航器来设计呢？**

同样是是先建好书签（无需再考虑按钮的插入与设计），并对书签进行分组。打开书签面板，按住Ctrl键选择应放入同一组的书签，这里是将本月、本季、本年三个书签选中，然后右键>分组，如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcrakssTXuLhicuxOb5m24LYA4mwtmAdXItsjeIFVcuu1sVV6z0Ok6RUh7YPdUWic3ppG4iakI9TDQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就将这三个书签放到同一组了，可以双击修改组名，这里命名为“本期”。

同样的方式，将另外两个书签分组，命名为“趋势”，这样就有了两组书签：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcrakssTXuLhicuxOb5m24T9TYUjDjVjQXo4ovYqDmU3Dpic9eQlWrP6M3n5Pps1ibe5S2m2F0upOQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后对于已经插入的书签导航器，选中它，在导航器格式设置面板中，展开书签功能，选择需要的书签组名，这里选择“本期”，而不是All：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcrakssTXuLhicuxOb5m24IicwjT7vdbZ6hlFJEK83tDychcSHcXuOicgWiaHCUjR7c101EO82xZQlg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

设置好以后，再看页面上的书签导航器，就会只显示“本期”这个分组中的三个书签了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNRcrakssTXuLhicuxOb5m24rgycL2Xhc4F4pJHZ7S4yzbkAiaeFTwPRrSVOIiatqCs89fqFBWAyc7eA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同样的方式，再插入一个书签导航器放到下面，只选择“趋势”的书签，这样就在这页报表中插入了两个书签导航器，分别切换不同的书签。

格式稍微调整就能得到下面这个局部切换效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNRcrakssTXuLhicuxOb5m24j32TIzyDRHano0gNlB4ZZq23ic0FTlqdHJ2RXFHemrxuhbiawnmmMUMQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

通过书签导航器来设置非常方便快捷，大多数情况下，你只需要灵活掌握[书签](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068219&idx=1&sn=b74e0d16ac61413a90fb5f7837dea112&chksm=8e0c75acb97bfcba745fe9ba7eb4ca2aa83d0af34a17668284170b97c68b2d3dc909dc9eb936&scene=21#wechat_redirect)的用法，而无需再单独考虑按钮的设置了。

通过[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080516&idx=1&sn=0290f2762815188f0b96e03f3f25fe7b&chksm=8e13a553b9642c45ecf32e51e95720e7f82a4ec9691bc00b6aaee95f12fd30e312557f5ce381&scene=21#wechat_redirect)以及本文，分别介绍了页面导航器和书签导航器的用法，灵活掌握这两种方式，以后你只需要轻松点击几下鼠标，就能快速完成报告的导航，帮你节省出时间着眼于更有价值的事情上去。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
