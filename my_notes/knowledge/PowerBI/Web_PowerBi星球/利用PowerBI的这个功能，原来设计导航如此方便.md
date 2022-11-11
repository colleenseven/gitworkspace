---
aliases: null
create_date: 2022-06-09T12:33:31 (UTC +08:00)
tags: 
pagetitle: 利用PowerBI的这个功能，原来设计导航如此方便
source: https://mp.weixin.qq.com/s/at2bEozVsWJuT0S4dQN9gw
author: 采悟
status: 未阅读
category: 
uid: 
---

对于一个多页面的PowerBI报告，导航是基本配置，之前一般是通过按钮来实现的，制作导航并不复杂，但是如果页面比较多，通过这种方式配置导航也是个比较耗费时的工作。  

其实PowerBI中已有页面导航器功能，它是2021年底发布的，经过几个月的迭代，它已非常好用，利用它无需单独设计按钮，就可以快速的完成导航设计，这篇文章就来介绍一下如何使用它。  

以下面这个报告为例，有四个页面，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1e2YLVtbEVXJ5qKoQENG7Q1W5vAcdEwuwYsgbCUbI4zvdEuh618IUhQA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中左侧的区域用来放置导航按钮，在“插入”选项卡上点击“按钮”，选择导航器：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1eAxmxk36cNkR1tCM0jplqyWupwVjU5lwFXicKUwSVxcnNHEPvTJpdzVw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这里有两种导航器：页面导航器和书签导航器，关于书签导航器，后面会专门介绍它的用法。这里先来看看页面导航器。

点击"页面导航器"，就会在页面上自动添加包括所有页面的一组按钮：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1eM5hfd8ia4aZLeiayE5t9gpdkhJ71DV1mJShAsfpicHViaAEZiaWc7eBSbgw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是默认的页面导航器的效果，点击按钮就可以导航到对应的页面（如果要在 Power BI Desktop 或在 Power BI 服务的编辑模式下测试页面导航器，需要按 Ctrl + 单击）。

并且页面导航器生成的这组按钮的是可以随着报告页面的变动自动更新的，这比单独用按钮来设计要方便很多，它有如下特点：  

-   按钮的标题与页面显示名称一致
    
-   按钮的顺序与报表页的顺序一致
    
-   所选按钮是当前页面
    
-   在报表中添加或删除页面时，导航器会自动更新
    
-   重命名页面时，按钮的标题会自动更新
    

由于它默认会将报告中的所有页面都添加一个按钮，当有些页面并不需要放在导航里面时，比如工具提示页面，这种情况下，可以设置导航器样式，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1eZ2joh3ibjhncgrZI2xibT2YkUicyu348SET2G2RXMcHQKwcuOUAXlDG8g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其实对于报告中的任意一个页面，如果不打算放到导航中，都可以先隐藏该页面，然后在这里关闭“显示隐藏页”就可以了。  

不过默认的页面导航器效果看起来比较丑，你可以通过设置导航器的格式进行一定的美化，比如更改形状：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1eW7lhiclr8xKeQQTbk2icC4N6JrBmy74ndV4gOInvFOw7P881r7ASaKoA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还可以更改布局，因为这个报告打算把它放到左侧的区域，方向改成垂直，并且填充改成0：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1eb46dwNXH7SqBSdXIA3Kh4Z8cBrvgQFCdbawWSvrwgU71GGsXzUGY3g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还可以像普通按钮一样，设置他们在默认、悬停、选定等不同状态的样式，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1e5fjzmtTibpFaWIqiciadY5jFgDicWwXN6uSW1ibIwPZucrCKzKtX6cEMU3A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

本示例中，将布局改为垂直、设置"默认"状态填充效果透明、“已选定”状态设置深色，就可以得到这样导航栏：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1eKk6gQVpanmB8FP2m4OyJW8b2YREVfR8wptMfbJIwS3KNJU77ia3RbyA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样看起来就接近手工设置按钮的设计效果了。

在这个基础上还可以进一步美化，比如复制一个同样的导航器，关掉按钮文本，已选定状态的填充色设置为醒目的橙色，置于原导航器的底层并稍微在左侧偏移出一点，就能做出下面的效果。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1eMVT31EzZz3d8D1DvvLxFo5pIVUvFW4dhUrWQvUmPS6KgNJIK0L6JhA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上下两个导航器是同步的，这样就能突出显示当前页面的按钮了。

一个页面的导航器做好以后，选中并复制页面导航器，粘贴到其他页面中，就制作好了一个简单而不失美观的页面导航器，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO1oPxE7Y532ybJjoNLBib1ey9dDCHy0qFRrh9x8qnlOuo2aibDpJibd1wbPM6YoNc4EHxhm2lq2apgw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

并且当新增页面时、删除页面，或者修改页面的名称时，这个导航系统也会自动更新，一次设计，自动扩展。

灵活使用页面导航器，无需繁琐的按钮操作，只需点击几次鼠标，就可以生成一个美观的导航系统，帮你大大节省报告设计的时间。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
