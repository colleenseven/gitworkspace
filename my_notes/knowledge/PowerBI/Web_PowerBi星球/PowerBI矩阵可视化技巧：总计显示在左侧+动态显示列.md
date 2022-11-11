---
aliases: null
create_date: 2022-03-10T12:00:20 (UTC +08:00)
tags: 
pagetitle: PowerBI矩阵可视化技巧：总计显示在左侧+动态显示列
source: https://mp.weixin.qq.com/s/QzEW6AmHN0qQSfWpOLLteA
author: 采悟
status: 未阅读
category: 
uid: 
---

PowerBI中的矩阵每个人都用过很多，经常碰到的一个问题是，如何将列总计显示到左侧，这种效果通过矩阵功能上的设置是做不到的，不过掌握一定的技巧利用DAX也可以轻松实现。

实现的原理和之前介绍的[复杂表格](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077653&idx=1&sn=3473232e3694cb2e90586c5fabbd695b&chksm=8e13ae82b9642794ca021808e9b3231ace4f66d8cf4dc22901042eb7d429ef06f586255ffc4d&scene=21#wechat_redirect)的做法类似，都是先构造个数据结构，然后利用度量值为结构上的每个类别赋值。

以这个矩阵为例，展示的是每个季度每个产品的收入，列总计很正常的显示在最右侧：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPWUr5T3vdB9qPAxicl3fnJ6x2iaPOHbRfDyQE4E6SbaUY8NmL5tBXnwiaRtsYsB4JQrPU4WrnrP16Yw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果想让总计显示在最左侧，需要在产品表中添加个“总计”项，构造出一个带总计的结构表。

新建一个表，为产品表新加一行序号为0的“总计”：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPWUr5T3vdB9qPAxicl3fnJ6EknCSJp26Vt0aI2NukmnEoNKDdn9Z0SvCWT5nU1gxbExdbg42IFcrw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后对产品名称按序号排序：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPWUr5T3vdB9qPAxicl3fnJ6LZicSw36paqqytQNYy0icwEZENYHpuopFcZAfhUglUsEJFJYMjmwJTeA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**总计的序号很关键，让总计序号比其他产品的序号都小，这样排序以后，才会出现在左侧第一列。**  

将新建的产品结构表与原产品表建立一对多的单向关系：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPWUr5T3vdB9qPAxicl3fnJ6vYMd9BvzC7WWawv72IZrCH1x29Zz6VUQtqmXQEWsb0Lq7lic7y8tsZQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

并写一个度量值：

> 产品收入  =
> 
> IF(
> 
>     SELECTEDVALUE('产品表 总计结构'\[产品名称\])="总计",
> 
>     CALCULATE(\[收入\],ALL('产品表')),
> 
>     \[收入\]
> 
> )

逻辑就是利用IF判断上下文，如果是“总计”，返回所有产品的收入，否则正常返回当前上下文的产品收入。  

然后将新建的产品结构表中的"产品名称"作为矩阵的列，上面的度量值作为值，就可以实现总计在前面的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPWUr5T3vdB9qPAxicl3fnJ66c7kX2JiaiaQXUEnJuNC8BM65bgAeQGBgiaW9Sn4hebwzUM1iaEBQgYibAg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**这里的总计是我们通过结构表构造出来的，至于矩阵本身的列总计，直接关掉不再显示就行了。**  

如果想突出显示总计列，可以利用条件格式为这一列添加个背景色：  

> 总计 背景色 = 
> 
> IF( SELECTEDVALUE('产品表 总计结构'\[产品名称\])="总计","LightCyan" )

然后把这个度量值放到"单元格元素"的背景色中：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPWUr5T3vdB9qPAxicl3fnJ6LeWjFZWWszRjWFOSc5jaCKe6xT4uogrulBKibKlem7IwmWxgSZnhO6A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

就可以实现总计行的突出显示：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPWUr5T3vdB9qPAxicl3fnJ6g7kzWVDSMM42B5DdIuawKPzHNlBNJMqMlic3oJhT2iagFoEW0tepuYOA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**如果产品名称特别多，直接全部显示出来，一方面不容易找到关注的产品在哪一列、另一方面也会降低报表的性能，能不能按需要来指定显示某些列呢？**  

其实只需要一个切片器和一个度量值就可以实现：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPWUr5T3vdB9qPAxicl3fnJ6c1VCSxMkiaIqo0CSONMhxb8mVbMPyU3bABnDAhvu1wQv8ibibmKoG4vVA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于判断切片器是否选择，突破默认的交互方式，之前也专门介绍过：[PowerBI切片器，原来还可以这样交互？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074281&idx=1&sn=ea825a10f8bb56815772997dcccfff08&chksm=8e0c5dfeb97bd4e8b6bf810457b5c579cf6633545260ce2097d21bc48e187bd88f49f3c528bf&scene=21#wechat_redirect)

将这个度量值放到矩阵中，并用原产品表（非产品 总计结构表）中的产品名称做个切片器，就可以实现下面的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPWUr5T3vdB9qPAxicl3fnJ6OTOwXyefgYwdD6p9BbKBMWmbHIlFkQ3xFqmTXaiagUsEEibWuceVRicNQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

切片器不选择时，只显示总计；选择哪些产品，就显示哪些列。这样用户就可以自定义选择浏览某些产品的数据了，并且总计列也是动态的计算选中产品的合计数。

本文用到的构造原理之前也介绍过，如果把这几篇文章熟练掌握了，关于矩阵构造的技巧应该都不是问题：

[Power BI矩阵格式设置13招](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071983&idx=1&sn=3fd379f7bf88141747ac9a09dc4273b7&chksm=8e0c44f8b97bcdee4cb068fd1e47e033629cf0734dd29c8341746d449372068dbb4e6d298cba&scene=21#wechat_redirect)  

[如何用Power BI设计复杂结构的表格？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077653&idx=1&sn=3473232e3694cb2e90586c5fabbd695b&chksm=8e13ae82b9642794ca021808e9b3231ace4f66d8cf4dc22901042eb7d429ef06f586255ffc4d&scene=21#wechat_redirect)  

[一文掌握Power BI矩阵的自定义配色](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078467&idx=1&sn=ad4e9834b50b19df4b0d79d156dfe0b3&chksm=8e13ad54b964244279a717fb8ddaa704cc3b5a1bf6f63fb377dd1f2d7c97f4c868b14d7799c5&scene=21#wechat_redirect)  

[一文掌握Power BI矩阵总计的自定义计算](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078406&idx=1&sn=3f64d35e34d0f9cd0d5483ee46bf124a&chksm=8e13ad91b9642487e4c2e64af7c944c76ef506eab1a9ecb731173a3cbfbf57b46da9c2cd855e&scene=21#wechat_redirect)  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
