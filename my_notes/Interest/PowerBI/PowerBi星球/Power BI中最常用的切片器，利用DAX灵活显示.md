---
create_date: 2021-09-03T22:43:44 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI中最常用的切片器，利用DAX灵活显示
source: https://mp.weixin.qq.com/s/JNng36DwI1FvGVFhARw22Q
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

PowerBI的切片器我们都不陌生，作为可视化必备控件，以前我们介绍过不少关于切片器的文章，比如：

[玩转PowerBI的切片器，看这篇就够了](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074560&idx=1&sn=7050c2194d5e0a5587ec6282ff17b4ad&chksm=8e0c5297b97bdb81d70e9a7ece3d0d557a1fe58fe7102ceedec734222a89777e8724f784acfe&scene=21#wechat_redirect)  

[利用PowerBI的这个控件，美化你的切片器](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073642&idx=1&sn=d4e57071dc6421b4bb2f0bc9fc1e51b2&chksm=8e0c5e7db97bd76b1e9de73326a5676b2b5aeca519c036bbc9a30ee7a15075145783e09c55b8&scene=21#wechat_redirect)  

[PowerBI切片器，原来还可以这样交互？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074281&idx=1&sn=ea825a10f8bb56815772997dcccfff08&chksm=8e0c5dfeb97bd4e8b6bf810457b5c579cf6633545260ce2097d21bc48e187bd88f49f3c528bf&scene=21#wechat_redirect)  

在实际使用切片器时，还有个问题是，切片器的显示项目默认是整个字段的所有项目，如何根据需要，不显示某些项呢？

比如在报告中放置一个日期切片器，由于我们对于日期表的要求是必须是全年完整的日期，所以切片器也显示的是所有的日期，包括未来的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPZ25FsSZGFo3F64UqXJ8jxBkMiaxLzXlSnTLDicF5MzQElYK7E6Jg3Xe9gY5nr05f1gr5aU3iaSqKzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在筛选器中，可以进行筛选，比如设置相对日期，只显示过去的60天，

但这种设置只能相对于今天、或者某个固定的日期来筛选，如果要根据最新业务日期来动态筛选，比如现在的最新业务日期是2021年8月31号，之后都还没有发生业务，切片器能不能不显示8月31之后的日期呢？

利用DAX做个度量值就可以实现。

> 日期筛选器 \=
> 
> VAR lastdate\_=MAXX(ALL('订单表'),'订单表'\[订单日期\])
> 
> RETURN
> 
> IF(SELECTEDVALUE('日期表'\[日期\])<=lastdate\_,"显示")

这个度量值先计算出最新的业务日期，然后判断日期是否早于最新日期，如果早于，则返回"显示"。  

将这个度量值放入到日期切片器的筛选器中，并设置为等于"显示".

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPZ25FsSZGFo3F64UqXJ8jxglFp0rfMRZZBqYKV59yYMj4ExzKia5db6iceVYdeXdHjldsXrtja67BQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样，该切片器就会只显示到最新业务日期：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPZ25FsSZGFo3F64UqXJ8jxS65icA1RPqicIFGqbmIaOk3icD6FKoZFp93lCsZ3OmibquicD4RvQ7EhYfA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果想让切片器显示相对于最新业务日期的最近2个月的日期，度量值可以这样写：

> 日期筛选器 2 =
> 
> VAR lastdate\_=MAXX(ALL('订单表'),'订单表'\[订单日期\])
> 
> RETURN
> 
> IF(
> 
>     SELECTEDVALUE('日期表'\[日期\]) IN
> 
>     DATESBETWEEN('日期表'\[日期\],EDATE(lastdate\_,-2),lastdate\_),
> 
>     "显示"
> 
> )

___

实际运用中，还有一种情况，如果有两个切片器，需要一个切片器根据另外一个切片器来确定显示的范围，比如之前做过的任意时间段对比（参考：[Power BI数据分析：任意时间段对比](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073999&idx=1&sn=43f01d0b797887bfa92b5a176f825611&chksm=8e0c5cd8b97bd5ce32e5baf3b8aa381157ddc852daa0f731f8e93fcf9c3df7bf17af3856496e&scene=21#wechat_redirect)），年度对比其实是没有必要对比两个相同的年度的，但切片器默认都会显示：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPZ25FsSZGFo3F64UqXJ8jxzvQc9o6nXd9QTDrFC5W1EpF3aazZAvtbdvaMvX21wj9D7AS6ibPe4wA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于这种情况，就可以设置为切片器不显示另外一个切片器的年度，写个度量值如下：

> 年度筛选器 \=
> 
> VAR slicer1=SELECTEDVALUE('日期表'\[年度\])
> 
> VAR slicer2=SELECTEDVALUE('比较日期表'\[年度\])
> 
> RETURN IF(slicer1<>slicer2,"显示")

将这个度量值分别放入到两个年度切片器的筛选器中，并设置为等于“显示”，然后两个切片器的选择项目就永远不会相同了：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPZ25FsSZGFo3F64UqXJ8jxuYpBmRN1Yqr1UAKxRiavL8jFlPgScmzJFkUicsEssajx53HeGPoiavvTw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

以上就是今天分享的技巧，利用DAX和筛选器，可以灵活控制切片器的显示范围。

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
