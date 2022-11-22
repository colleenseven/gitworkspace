---
create_date: 2021-08-31T22:44:12 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI的这个功能，每个人都用过，但是我建议你以后禁用
source: https://mp.weixin.qq.com/s/itQaX1ncMHErQOnYjhjfAQ
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

在本文开始之前先看看两个在使用PowerBI的过程中，经常会碰到的两个问题，你肯定也见过。

___

**Q：**

想看每天的销售额，本来放的是一个日期字段，却突然冒出来很多列，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OMad0O08zgFdRica4SxgbzCE7syiaD0xYF5ywvS18nK1asdqUOeA43TGw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并且月份还是英文的，想改成中文的都找不到地方改，去生成表格的字段里面查看，也会发现，一个日期列自动出现了这个层次结构，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OJApCHrXfvt9hovUb4yzex8jWb5v0nniauCcUUhcg53Uc6bjvoeryRaw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

那么如何解决这个问题，不显示这个层次结构呢？

**A:** 右键上图中的日期字段，去掉“日期层次结构”的勾选，改成“日期”就可以了。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4Ocjbd4O8vpqgKtvfglCBI3Mzf5cDicZFTAvian0r7TbGyh1wqgXicleEkw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**Q：**

写DAX用到日期列时，总是会蹦出这样的提示，比如：

如果你不小心选了.\[Date\]，结果很可能是莫名其妙的，也许数据表中最后发货日期是2021年8月31号，可是计算结果却是2021年12月31号，这怎么解决呢？

**A:** 在公式中删除.\[Date\]。

___

这些情况是不是非常熟悉，虽然通过上面的方式，可以将遇到的现有问题解决，但并没有得到根本的解决，下次你依然还会继续碰到。

**其实上面两个问题看起来不同，但其背后本质的原因是相同的，根源就在于PowerBI中的一个功能：自动日期表。**

如果满足以下条件，Power BI Desktop 会为每个日期列创建隐藏的自动日期表：  

-   表存储模式为“导入”
    
-   字段数据类型为“日期”或“日期/时间”
    
-   列不是模型关系中的“多”方
    

该功能本来的意图可能是为了提供方便，即使不建立日期表也能快捷的使用时间智能函数，但在实际使用过程中，便利几乎没有享受到，而出现的问题倒是不少。

**由于自动日期表是隐藏的，列的格式无法自定义调整，也不能根据需要扩展增加其他维度列，DAX无法直接引用它们（只能间接引用），他们还总是在你不防备的地方冒出来，一不小心就让计算结果变得莫名其妙。**

并且如果模型中的日期列很多，系统分别为每个日期列都创建个自动日期表，这样对报告的性能也会有影响**。**

基于以上原因，**我建议你在使用PowerBI 的时候，禁用自动日期表**，在选项中，将全局和当前文件中，这两个地方的勾选都去掉：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4Oa0xJvtCOotFXKaTAC1xXB2GhbDG4xEMHO5jA4CkzodicunpoVu4ibxibA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OvrURLox7kKAXur667CG1fI4hX2PfFVUj30W5XPAticRfq5ia2HCiaPVJw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样设置以后，不仅本文件不会再出现内置日期表，以后新建的pbix文件也不会再出现。

禁用以后，之前基于这些内置日期表创建的图表或 DAX 表达式将不再正常工作，如果有报错的地方，需要手动调整。

如果你的模型需要用到日期表，应该根据业务需要手动创建一个，可以参考这篇文章的DAX公式，帮你轻松制作一个日期表：[**分享一个更实用的Power BI日期表**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076559&idx=1&sn=e00814afa6a2013e3ba3a19cfb575f39&chksm=8e13aad8b96423ce61ca80169b35047204be5c7e4750491f84d7ff327eba9c093c9aa9a829f2&scene=21#wechat_redirect)

___

关于内置的日期表，如果说有一个方便的地方，可能就是日期层次结构，很多人都喜欢用这个结构，而禁用掉以后，就不会再自动出现，如果你需要使用这种结构，可以手动建立，方法如下。

为日期表中的日期列建立层次结构，可以右键日期列，点击“创建层次结构”：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4ONdKKpQkzUg6le0uibzkTVqYib3lrchibJ1YGuiaOKQueHd5H49MhSPdDsg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就在日期表中增加了一个日期层次结构：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OovyX3wKkVSw0iaOs9XREVOic7XCHk6mkbBfkkCyYZFic5Z825aPNRZf3g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

想让哪几个字段放到日期层次结构中，就右键该字段，比如将年度名称添加到已创建的日期层次结构中：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OqjI1IkIobErW8hhTxVqFEhO5vNJgMYNAFLDI2S5AzbUrhFYwxZ3aqg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同样的方式，将季度名称、月份名称和日放到层次结构中，就可以获得和内置日期表类似的结构：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OPJBYicfnZtlchGYEkD2zwU571ZM4ibSTfPlqD69Vm9kOE52JpOaEd7sA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

用这个结构做可视化，也可以得到这样的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPUabZXugXKNdmeUzxwJM4Ob69r3SgMm2KowlF1vRiaic9P1KYtVtPjsnC4IyPNFI4PJRpOAxO0JzIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

并且这个月份名称还是中文的，其实我们**可以根据需要将日期表中任意一个维度加入到这个层级中，相比自动的日期层次结构灵活多了，**用这个层次结构做图，也是可以向上向下钻取的。

并且上面创建层次结构的方法并不局限于日期表，任何一个表，如果你需要层次结构，都可以创建。

关于自动日期表就介绍到这里，希望帮你解决了在使用Power BI过程的一些疑惑。

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkvUibMVjf4z1bY0MYFh7lAkqrcHiaEHE4UicvjJjibpmkxJjc4TDlVO04qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OyUpTibBJjoq1jk8CzVZJz6s4nJRW1ViammT4ecqAJ7iapDccKNNrwtLYQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077212&idx=1&sn=bb3dac9becf80b5d929e5dc8405158dd&chksm=8e13a84bb964215d6362f78768cdefa18def4dfc8cd5c14f075442431604ed9c9729e4051a4b&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
