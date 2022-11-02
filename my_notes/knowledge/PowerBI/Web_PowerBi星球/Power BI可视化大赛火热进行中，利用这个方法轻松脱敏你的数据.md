---
create_date: 2022-04-22T11:53:52 (UTC +08:00)
tags: 
pagetitle: Power BI可视化大赛火热进行中，利用这个方法轻松脱敏你的数据
source: https://mp.weixin.qq.com/s/GwxNYTfkn9gbGCxslkVOUw
author: 采悟
status: 未阅读
category: 
uid: 
---

第五届PowerBI可视化大赛已开启，如果你有意参赛，请进入这篇文章中的链接报名：[决战数据之巅！第五届Power BI可视化大赛开始报名！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079783&idx=1&sn=4d07e18f0efe2a77a3fc3eb8a0a2f2e7&chksm=8e13a670b9642f66bc19be6bf60a2751f5a3c9508edd5eec462a5e25b7182c54b4fe88e3f8c3&scene=21#wechat_redirect)

关于参赛的数据，可以使用自己的数据，也可以使用组委会提供的数据。

你可能想用自己的数据（我也建议如此），毕竟对自己的数据结构以及其中的逻辑关系非常熟悉，可以更快的做出一个可视化报告，甚至你已经有了现成的报告，只需要集中精力修改美化就可以了，毕竟这是可视化大赛，报告的外观美观性评分占比最高（60%），这样不仅可以节省宝贵的时间，获奖几率也更大。

但你可能又担心自己的真实数据泄露，其实大可不必担心，因为大赛组委会明确要求数据必须脱敏：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNTv7Kgg58ib1Y4O4gzlT3PEaGOSgiaL9Pic5UnHrqputYWibv6k0ZAfjHgrXJiaQBMH3TyvTEflbfibMrQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

所以你要做的，就是先对自己的数据脱敏，然后集中精力设计可视化报告。

数据脱敏是将数据中的敏感信息进行一定的变形处理，抹去不适合对外展示的信息，这是对数据的保护，也是对你个人的保护，以免陷入不必要的纠纷。

那么如何脱敏呢？  

方法有很多种，这里介绍一下如何利用Power Query来实现对数据的快速脱敏。以这个简单的模型为例，其中有一个订单表和两个维度表，客户表和产品表：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyMJ2OlzbXcGf64pDicbNoyIEIYnchnYeTEfp3V7wgia1MiaaFglqLIVvIA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**一、订单表脱敏**

原订单表是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyibraO4icy5syTDfUD43MNZwVvEjzJorypGFz6Sx7tzRkmMTDFKkoOYRw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于这样一个数据，可以从以下几个方面进行脱敏：  

**1\. 缩减数据量**

可以通过删除行的方式来减少数据量，  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyLpkzRw5hMWAVDrAJHcd2JEuqkabvCG5lC1vrs8zBiavT9ewSicBIZNqQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

选择“删除间隔行”，如果要减少80%的数据量，可以这样来设置：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyNVgkRL10J3XLVtvgkyDTsbThdAuvwG6zongreianx9yFQ73Zj9XgDIg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上图这几个数字的意思是，从第1行开始删除8行，保留之后的2行，然后再删除8行、保留2行，依此类推……，通过这个方式，就能够将数据量大幅降低，只有原来的20%。

你可以根据需要填入适当的参数来缩减数据量，**这种间隔穿插删除的好处是，每个维度都可以保留部分数据，而不是简单粗暴地直接把某些年份或者某些产品的数据全部删除。**

**2\. 订单日期脱敏**

可以增加一个自定义列，随机将每个日期移动N天：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyfyXNibFuXD2fQ0pYEHjVbg4KDZlP4q6fEvtHcJd0KjcwgxQ3Llxuuzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

Number.RoundUp(Number.RandomBetween(0,10))可以生成1到10随机的整数，然后利用Date.AddDays将每一个日期往后移动相应的天数。

**3\. 销售额脱敏**

同样可以利用上面的M函数生成随机数，下面的自定义列是将原来的订单额乘以一个随机的系数（1.1到1.2之间）：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOyb6uZa9XVianIR1r1pwyeaIYp4aDGFQZaVGfPM3krC6IoYbxP6Zj211YVZckMbLvYOliaCBFWicu9w/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**这样随机的好处是，既抹去了具体金额，但整体上还保留原有数据的规律，对于可视化效果不会产生明显的影响。**

然后把原来的订单日期和销售额列删除，就得到一个脱敏后的订单表：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOyb6uZa9XVianIR1r1pwyeahQ4YZpPuApc3GPEl5kvrPDvF42GtRrUCsaWNvAjMvn2Ye5tqXTjopQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**二、客户表脱敏**

原客户表：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyEHl2KWyJ1KcWmvx8ECMzn8GX4QsibgzD0cRrOaBlMnxqeM71ocHIPEQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于这个表，真实的客户姓名肯定不能泄露，可以将客户姓名做一下变形，用下面的写法添加一列来代替姓名：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyJH2zp7eee0OHvaBxT3Hl7XhSWFprj3ZkEDyFEMzwIFWDmo0qsoJe8g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这个公式将原来的客户姓名替换为客户1、客户2……  

然后将原来的客户姓名列删除，就得到了脱敏后的客户表：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyDOpLRxUfbJriaO2TrMHEGiaYiaIdBTVmprddrID9oNGrMDhbGU0HvsbDA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**三、产品表脱敏**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyN8ia8OyvNXVz9wgzLG2JEic5NZh1RPswxcn6GUiaia1S1HENLQu29lZibZg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于这个产品表，同样可以和客户表的处理方法一样，生成一列产品1、产品2的产品列来代替真实的产品名称。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJN0ZiaAl9YH4czFscta9zquyUBtl0zeWcgND31hTReib36IKaHuTJZRjPfgltr3StViabgGibUyMzgwoQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

通过以上的操作，你的数据就变得“面目全非”了，但这样处理以后，你还不能在现有的基础直接加载到模型并制作报告，因为powerquery会保留每个处理步骤，通过查看前面的步骤依然可以看到脱敏前的数据。

所以最后还需要是将脱敏后的数据导出来，才能彻底与脱敏前的数据断开联系，你可以参考这个方法将PowerBI中的数据导出到Excel：

[PowerBI中的数据如何导出到Excel？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067701&idx=1&sn=b25ce0581c897a817fd1523915cd8d9f&chksm=8e0c77a2b97bfeb4c22b58f13accf44029c2fd4ccc6cecd318eceef48bc44deb03cc2806e950&scene=21#wechat_redirect)  

如果数据量大、表比较多，还利用DAX Studio，将模型中的数据表一次性导出来：

[DAX Studio：你迟早会用到的几个功能](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068433&idx=1&sn=a7024f9924b5d498447cb209c5fac222&chksm=8e0c4a86b97bc39093d64194865a45865432b07fb14dd6d822519c60be7bbe1c8523e6e3fe61&scene=21#wechat_redirect)

脱敏后的表导出来保存，当你需要使用脱敏数据做报告，或者使用脱敏数据描述问题的时候，就可以直接导入使用了。

关于数据脱敏，上面只是几个简单的思路和处理的方法，并不是必须对每一列或者每个维度都要这么做，你可以根据实际情况选择对某些关键信息脱敏，并不局限于这些方法，甚至也不局限于PowerQuery，用Excel同样可以做到。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
