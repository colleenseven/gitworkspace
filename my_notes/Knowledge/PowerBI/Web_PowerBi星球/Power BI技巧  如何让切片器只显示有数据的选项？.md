---
create_date: 2021-10-19T12:59:34 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI技巧 | 如何让切片器只显示有数据的选项？
source: https://mp.weixin.qq.com/s/DeSFu8UuiRLE58he3CMi9w
author: 采悟
status: 未阅读
category: 
notes: False
uid: 
---

使用PowerBI做数据分析的基础，要先建立合适的数据模型，将数据表分为维度表和事实表，在做可视化时，坐标轴、切片器等上下文应该来源于维度表的字段。

**但是很多人不喜欢用维度表，其中一个原因是，如果用维度表做切片器，包含的选项太齐全了，无论是否有数据，都会显示出来，如果选项很多，选择起来会很费劲。**

不过这不应该成为不用维度表的理由，只有用维度表，才能更好、更快以及用更简单的DAX来实现分析需求；对于上述问题，即使用维度表，也是可以轻松解决的，只需要在筛选器中加个条件就可以了。

最常见的维度表当属日期表了，为了能够正常使用时间智能函数，日期表必须是整年不间断的日期，那么当使用日期表中的日期列做切片器时，就会显示全部的日期，包含没有业务发生的日期：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPfcfKwxTee294Fia0u57FKhxBGhA8HvVAao18UN8GFOH2Mhfp48VydFSA16DsmYxfPFYbTdj42BdQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

很多人就是因为这些日期很多都是无用的，所以选择了用事实表的日期，其实大可不必，通过一个简单的筛选条件就可以解决这个问题。

如果想让切片器只显示有数据的日期，可以写一个度量值，计算事实表中的行数，比如模型中订单表的行数：

> 订单数 \= COUNTROWS( '订单表' )

将这个度量值放到该切片器的筛选器中，筛选这个度量值大于0的数据：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPfcfKwxTee294Fia0u57FKh0HO0aSQaePMicp36ucje7qc9kaYAPeM6jOVibdZb7FcmwhqlBkCuFjmQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因为该度量值会计算每个日期所对应的订单数，用上述筛选器的结果，就是只有该日的订单数大于0时，才显示出来：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPfcfKwxTee294Fia0u57FKhVbZjDd0Ytyic95KicE06LRFNuMC7KRjAar3VpeAtFNZ7qWcelC8HuMIA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样就解决了这个问题。

如果报告中还有个产品切片器，可以在这个切片器的筛选器中，也加入上述度量值的筛选条件，这个度量值就会计算每日每个产品所对应的订单数量，如果当日没有销售某个产品，则它在产品切片器中也不会显示出来：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJPfcfKwxTee294Fia0u57FKhu1CyTfbuaP3JoHwMtAcT4UPHSANejAhT5GVjGdvR2Lwa0J2J1fBcwQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

**这样就做到了，不仅日期切片器只显示有数据的日期，产品切片器也会动态的只显示有数据的产品，通过这样的设计，可以帮用户避免很多无效的点击交互。**  

对于日期切片器，如果不想显示未来期间的日期，除了以上筛选器的方式，还有个更灵活的方法，就是之前介绍的，在日期表添加计算列：  

[Power BI设计技巧：切片器的动态筛选](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074134&idx=1&sn=351c14436442ed68b0249ee1e4f5de72&chksm=8e0c5c41b97bd557d4347f0b6d9dc33ea87166d5de716c34cf68dd9ddece57d2ee2195847b1a&scene=21#wechat_redirect)  

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYCTV9SBx5LXD4kp3icA9LouW3YN2z2njBWWQzM1zia9Fbeky0fdIpNakw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和3800+ 爱好者一起精进~**

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
