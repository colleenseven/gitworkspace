---
create_date: 2022-05-04T11:52:19 (UTC +08:00)
tags: 
pagetitle: PowerBI可视化设计技巧：页内导航
source: https://mp.weixin.qq.com/s/K_xFcNiHszB-_1mOt3Dimw
author: 采悟
status: 未阅读
category: 
uid: 
---

在进行PowerBI可视化报告的导航设计时，一般是利用页导航或者书签的方式来实现的，经常有人问这两个功能有什么区别，既然都可以实现，为什么要设计两种方式呢？  

简单来说，页导航只能导航到某个页面，如果你的报告确实是这个需求，那么利用页导航功能十分方便，直接设置按钮的操作属性为该页的名称就可以了。  

但是利用书签实现就没有这么方便，必须先建立书签，然后才能使用，但是并不能因为书签多了一个步骤，就觉得书签无用，恰恰相反，书签的灵活性以及应用场景要远远超过页导航。

**书签不仅仅能导航到某个页面，还能在一页内任意跳转，本文就来认识一个书签能实现但是页导航无法实现的应用场景：页内导航。**

比如下面这个报告，只有一页，通过点击各个按钮，分别跳转到对应的数据图表：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2dk7iagThG1NwU65N3uiaCvqlzwXoCJ6oSWlibPOuuabqJ2X49O9TDeIPQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这种设计的基本思路其实就是之前介绍的用书签来显示不同维度的数据趋势：

[利用书签，轻松显示不同日期维度的数据趋势](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074411&idx=1&sn=7f8b45e40cb2c41710fe3a6cc69f1dbd&chksm=8e0c5d7cb97bd46a42ce531b14336ff340cd7e3cd5e9c6dd24b5feda5481609b790e9980cb4c&scene=21#wechat_redirect)  

这里进一步美化，设计成页内导航的效果，关于三个图表和按钮的制作这里不再重复，这里接着链接中的文章的步骤，介绍一下页内导航效果的简易做法。

**1、将不变的元素设计为页面背景图片**

利用页面背景，可以更快速、更美观的设计报告效果，这里将不变的元素，比如主要的布局框架，以及页内导航的几个灰色按钮都设计到背景图片上，用PPT就可以做到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2fWgymZRia53biaUCUygYKLaF6dibKKBME6OicduX78IhUDSyePKHJ1Pb5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后将PPT导出为图片，并插入到页面背景中，将图表和控件放到对应的位置上，就有了下面这个报告：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2icicCy6ODRiaZ76oJmyRgwvCMeRko3L7lAaPFIIANUX2GicqvjpAEUT3Tg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

利用“本月”、“本季”、“本年”这三个按钮也可以直接切换，不过为了可视化效果切换更自然，下面再进行一下美化。  

**2、插入当前页面的醒目图标按钮**

可以在PPT中设计一个和上面页面背景中的灰色图标尺寸相同，但是颜色更醒目的图标，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNicGqnNoVZ636SThJssJKSh6ZrhvQYH1nUWibAzG38Y5A2N1weGhbY9M7yVgs3endKRZTatk6fHIbA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后导出为图片，并在PowerBI中通过插入>图片的方式，插入进来，作为当前所选的按钮效果，因为有三个切换图标，所以插入三个一样的，放置到切换按钮上面，并设置“置于底层”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2cuQicov3Hb8ULJzsxU5Ke0YuKtqhuOoUl4KIWafKlUbDDHPTxAgTsqg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3、设置图标状态，并更新书签**

为了只显示当前数据对应的导航图标，将其他两个醒目图标隐藏，比如在选择本月数据时，隐藏“本季”和“本年”的图标。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2o3m9slkrUYu9ZO2ib7uSFo1U2jTDEq4DOp8dx9sib2XkLbh30a8iacH4g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就看起来，本月的按钮突出显示，而其他两个按钮呈灰色，可以直观看出图表显示的是哪个导航的数据。

然后更新本月的书签。

同样的方式设计本季和本年的书签，页内导航的效果就制作好了，也就是本文开头的效果。

希望通过本文的介绍，你能够理解页导航和书签的不同之处，并学会灵活使用书签的这个应用。  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
