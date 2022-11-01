---
create_date: 2022-08-28T12:21:10 (UTC +08:00)
tags: 
pagetitle: 在Power BI中如何通过经纬度来计算距离？
source: https://mp.weixin.qq.com/s/6FlIiX7K1TLt-PDJHOW_4A
author: 采悟
status: 未阅读
category: 
uid: 
---

经纬度是某个地点的坐标信息，通过经纬度数据就可以计算出这两点之间的直线距离，PowerBI能不能实现这种计算呢？  

其实这是一个数学问题，也就是计算球面上两个点之间的距离，关于这个计算，有专门的公式，如果想在PowerBI中计算，只需要将它用DAX函数表达出来就可以了。

比如下面这个数据，是几个主要的城市经纬度坐标信息：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgyXGG3p3PTLE1TO3zaia4w2DeBkISF2MD9NKtwF3A2W5zEBt8iaiaiaJnEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

注: 每个城市都是个面积很大的区域，上述经纬度只是用其中的某个位置点来代替而已。

假如要计算上面的每个城市距离北京的直线距离，应该怎么写呢？这里直接列出这个度量值：

```
与北京直线距离/km = 
```

其中RETURN后面的就是计算公式(6371是地球的半径)，主要是利用了DAX中的数学和三角函数的组合运算，对数学感兴趣的同学可以研究这个公式的原理，不感兴趣的直接套用上面的公式就行了。

结果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgw53gBJNp79SVib9EvfLMnTs4xJ7Xx4r6tT06gXwLiaDCo6lHj9eQNspA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

最后，需要说明的是，上述公式只是近似的计算，一方面受经纬度本身的精度所限，另一方面地球并不是个完美球体，从赤道到两极地球的半径是有差异的，因此计算结果与实际会有些许误差。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
