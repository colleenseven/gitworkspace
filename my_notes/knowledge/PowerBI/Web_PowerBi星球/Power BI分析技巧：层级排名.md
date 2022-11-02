---
create_date: 2022-05-16T11:50:17 (UTC +08:00)
tags: 
pagetitle: Power BI分析技巧：层级排名
source: https://mp.weixin.qq.com/s/fH9IUk-gPs881K6514tXCg
author: 采悟
status: 未阅读
category: 
uid: 
---

以前曾经介绍过[层级占比](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068912&idx=1&sn=70e9083b581019385e8877d4a91e5a26&chksm=8e0c48e7b97bc1f159d60622393ab8b7a30c3cde30006d465b10cf005ecb58238e84ab77415c&scene=21#wechat_redirect)，也就是父级字段显示该层级值占总体的比例，子级各明细项显示占所属父级的占比。  

最近遇到有人问能不能按层级进行排名？以下面这个矩阵为例来说明。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN9HCk0Ls3zNhu2gQYARG081vA0ibl065IedHibaSgkA0ibQeNmEvaDkXFLXWYIicaicnMYCfQe7VvianlA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个矩阵有两个层级，产品类别和产品名称，按销售额来排名，假如想要的排名逻辑是，**当上下文是产品类别时，在产品类别的范围内进行排名；当上下文是产品名称时，在该类别内的产品中进行排名，这就是一种层级排名。**  

其实思路与层级占比是一样的，也是判断当前的层级，然后对应返回当前层级内的排名。

关于排名的计算，之前专门介绍过：

[这几个示例，帮你深入理解RANKX排名](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068781&idx=1&sn=4f7d7abed75b6db6cae3b23a45e7dfbe&chksm=8e0c4b7ab97bc26c2303edcd22dad9261981486689833504f129603f5b20a7b8f8d3669517e6&scene=21#wechat_redirect)  

其中已经写好的类别中产品绝对排名和层级绝对排名：

> 类别中 产品绝对排名 = 
> 
> RANKX(ALL('产品'\[产品名称\]),\[销售额\])
> 
> 按类别绝对排名 = 
> 
> RANKX(
> 
>     ALL('产品'\[产品类别\]),
> 
>     CALCULATE(\[销售额\],ALLEXCEPT('产品','产品'\[产品类别\]))
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN9HCk0Ls3zNhu2gQYARG08J8sGbceKya6LkGn1zgPKkwicznBUAJdVa6DzzEPbDUhsRv3PkcE2iauQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

\[类别中 产品绝对排名\]是每个产品在本类别中的排名，但在产品类别这一层级，排名都是1，这里需要让产品类别层级的排名也正确，也就是度量值\[按类别绝对排名\]返回的结果，只需要将这两种排名整合到一起就行了：

> 层级 绝对排名 =
> 
> SWITCH(
> 
>     TRUE(),
> 
>     ISINSCOPE('产品'\[产品名称\]),\[类别中 产品绝对排名\],
> 
>     ISINSCOPE('产品'\[产品类别\]),\[按类别绝对排名\]
> 
> )

这里依然是利用ISINSCOPE函数来判断层级，返回对应的排名，效果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN9HCk0Ls3zNhu2gQYARG08G887CM0nCtAsNwkcqlEh38UOJgJ8XopbUs2eoicPWtOSFJB12BLTFOQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就实现了每个层级都满足分析需要的层级排名。

上面的排名是层级的绝对排名，这里仍然可以按照之前关于相对排名的思路，再做一下层级的相对排名。

> 类别中 产品相对排名 \= 
> 
> RANKX(ALLSELECTED('产品'\[产品名称\]),\[销售额\])
> 
> 按类别相对排名 \=
> 
> RANKX(
> 
>     ALLSELECTED('产品'\[产品类别\]),
> 
>     SUMX(ALLSELECTED('产品'\[产品名称\]),\[销售额\])
> 
> )

（关于按类别相对排名的度量值，这个写法也是对[之前文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068781&idx=1&sn=4f7d7abed75b6db6cae3b23a45e7dfbe&chksm=8e0c4b7ab97bc26c2303edcd22dad9261981486689833504f129603f5b20a7b8f8d3669517e6&scene=21#wechat_redirect)的修正）

当筛选部分产品时，其排名的效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN9HCk0Ls3zNhu2gQYARG08qw5MibC1Y5iaj8KfWAgwC3TEVaIviaiaMwGFtPib8W1eYshbopkhYicYeAFw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后对层级相对排名，还是上面的思路来写度量值：  

> 层级 相对排名 =
> 
> SWITCH(
> 
>     TRUE(),
> 
>     ISINSCOPE('产品'\[产品名称\]),\[类别中 产品相对排名\],
> 
>     ISINSCOPE('产品'\[产品类别\]),\[按类别相对排名\]
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN9HCk0Ls3zNhu2gQYARG08dhljmA3LVLDqHS1AoalF1cmVs178eotMt03FS2jxxIiaqboXZxV7Ubw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就实现了，无论上下文选择哪些产品，都可以动态地实现在所选择的范围内进行层级排名。  

以上就是两种层级排名的思路，先按逻辑先对每个层级分别排名，然后利用SWITCH+ISINSCOPE函数判断层级，将多种排名逻辑整合到一个度量值里面，就可以轻松实现。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
