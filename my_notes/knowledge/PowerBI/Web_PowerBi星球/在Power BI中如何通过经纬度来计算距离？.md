---
notes: False
aliases: null
create_date: 2022-08-28T12:21:10 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: 在Power BI中如何通过经纬度来计算距离？
source: https://mp.weixin.qq.com/s/6FlIiX7K1TLt-PDJHOW_4A
author: 采悟
status: 已完成
category: 浏览文章
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
VAR longitude=[经度]
VAR latitude=[纬度]
VAR longitude_bj=CALCULATE(MAX('数据表'[经度]),FILTER('数据表','数据表'[城市]="北京"))
VAR latitude_bj=CALCULATE(MAX('数据表'[纬度]),FILTER('数据表','数据表'[城市]="北京"))
RETURN
    2*6371*ASIN(SQRT(
        POWER ( SIN ( (latitude - latitude_bj) * PI () / 360 ), 2 )+
        COS ( latitude * PI () / 180 )* 
        COS ( latitude_bj * PI () / 180 )*
        POWER ( SIN ( (longitude - longitude_bj) * PI () / 360 ), 2 )
    ))
```

其中<mark style="background: #FF5582A6;">RETURN后面的就是计算公式(6371是地球的半径)</mark>，主要是利用了<mark style="background: #FF5582A6;">DAX中的数学和三角函数的组合运算</mark>，对数学感兴趣的同学可以研究这个公式的原理，不感兴趣的直接套用上面的公式就行了。

结果如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgw53gBJNp79SVib9EvfLMnTs4xJ7Xx4r6tT06gXwLiaDCo6lHj9eQNspA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

最后，需要说明的是，上述公式只是近似的计算，一方面受经纬度本身的精度所限，另一方面地球并不是个完美球体，从赤道到两极地球的半径是有差异的，因此计算结果与实际会有些许误差。
