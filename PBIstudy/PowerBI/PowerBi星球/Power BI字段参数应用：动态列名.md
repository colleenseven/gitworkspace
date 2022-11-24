---
ZK: Origin
notes: True
aliases: null
create_date: 2022-06-14T12:32:27 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: Power BI字段参数应用：动态列名
source: https://mp.weixin.qq.com/s/6DAkVAMxusfsPHoW0XVf3Q
author: 采悟
status: 已完成
category: 精读文章
uid: 
---

DAX:: NAMEOF， CALCULATE,MAX,TODAY

---

最近碰到一个星友的提问，他结合[这篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074772&idx=1&sn=f13557e739a5b0304696c1b9213c09c2&chksm=8e0c53c3b97bdad5d606da03d4723cbdb822d3a5faa7d6b2b0d4fa4e8268bad5fe2d58ddfac8&scene=21#wechat_redirect)（[无日期上下文如何计算同比环比](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074772&idx=1&sn=f13557e739a5b0304696c1b9213c09c2&chksm=8e0c53c3b97bdad5d606da03d4723cbdb822d3a5faa7d6b2b0d4fa4e8268bad5fe2d58ddfac8&scene=21#wechat_redirect)）的思路，已经建好了本月、上月、上年同期以及环比、同比数据这几个度量值，用矩阵展示每个类别的数据如下图：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMGAlWib41ndKI9nSgeMibKKMwDVGcmumq7pxyXspBtpL8X4x19ObbAkcF7NoaicZS2vOfG332OsezUg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

想在此基础上为进一步设计：

-   为所有的数据列添加一个表头，命名为“收入”；
    
-   将本月、上月等显示为具体的月份，比如现在是2022年6月份，本月就显示为202206，上月显示为202205，并且月份是可以动态变动的，到7月份，本月自动显示为202207。
    

想要实现的效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMGAlWib41ndKI9nSgeMibKKMeT2DVwmggdZ045Zkib5oOF1HQeWgicjvyQJPmR0tHXkuMUJNwJCyeA2Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于第一个需求很简单，利用之前介绍过的构造复杂表格的思路就可以做到：

[如何用Power BI设计复杂结构的表格？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077653&idx=1&sn=3473232e3694cb2e90586c5fabbd695b&chksm=8e13ae82b9642794ca021808e9b3231ace4f66d8cf4dc22901042eb7d429ef06f586255ffc4d&scene=21#wechat_redirect)

而对于第二个需求是个难点，在5月之前很难做到，不过现在利用<mark style="background: #FF5582A6;">新的字段参数功能</mark>，上面这两个需求都可以轻松实现，下面介绍一下实现步骤。

#### **1\. 新建字段参数**

利用已经建好的度量值生成字段参数。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMGAlWib41ndKI9nSgeMibKKMIqkdBwPx2t4YTDuRAZNlfY6NOdZJiahh6aA28reoztbJwGw3bSXBW4A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于字段参数的基本用法请参考：[Power BI字段参数介绍以及常见应用场景](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080273&idx=1&sn=b985ea8a53854f41a1ba75c0585cb3cd&chksm=8e13a446b9642d5085b1590f38ca7dd36c085269ae2d5d0fe75e09c57fc1ae270158d15d79db&scene=21#wechat_redirect)  

#### **2\. 为参数表添加一列**

打开参数的DAX表达式，手动添加一列，每一行都是“收入”。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMGAlWib41ndKI9nSgeMibKKM5K8BObs9tugC015aU2flj4NDqJQzOGdzGvxj7dya98RlZia9RQpueAw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后将参数放到矩阵的【值】中，手动添加的列放到矩阵的【列】中，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMGAlWib41ndKI9nSgeMibKKMQDia9opGQF5wQIjgKLcA5icqcWCFD2VctEB308pzlibyEGBsKzG2yicxlw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMGAlWib41ndKI9nSgeMibKKMTqIopjBe9Jwtq1L6nnIIuBbjE2uT8EzMmmicDDFnuiboRFMwgatVwNEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就<mark style="background: #FF5582A6;">添加了一个表头，实现了第一个需求</mark>。

左上角自动显示了该列的列名，你可以双击【列】中的字段，将它直接修改为空格，就不会显示了。

#### **3\. 修改参数表中的参数名称**

<mark style="background: #FF5582A6;">自动生成的字段参数，名称默认是度量值或者列字段的名称</mark>，<mark style="background: #FF5582A6;">这个名称是静态的文本，不过它也是可以利用DAX来调整为动态的变量。</mark>

这里接着修改参数表的公式如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMGAlWib41ndKI9nSgeMibKKMchSpQqcz7ibnWUNG91lht5lYmFQ22ndgzCZvEVuAQQg0kY33KsSgGnQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

（点击查看大图）  

这里的逻辑是<mark style="background: #FF5582A6;">先利用变量找出本月、上月、上年同期对应的年度月份，然后将参数表的第一列，修改为对应的变量名，其中同比和环比也在字符的前面加上对应的年月，以便更清晰的显示出具体是哪个月的指标。</mark>

这样修改后参数表的第一列就变成了具体的年月，矩阵也自动变成了需求的效果：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMGAlWib41ndKI9nSgeMibKKMeT2DVwmggdZ045Zkib5oOF1HQeWgicjvyQJPmR0tHXkuMUJNwJCyeA2Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

参数的名称利用TODAY函数来获取的本月和上月的名称，那么随着时间的变化，这些列名也会自动的调整。

利用<mark style="background: #FF5582A6;">字段参数这个特性，不用单独构造结构表，也可以便捷而灵活地来设计一些个性化的中国式报表了</mark>。
