---
create_date: 2022-11-24T23:51:29 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI如何展示本地图片？原来这么简单
source: https://mp.weixin.qq.com/s/CuyVIsH9eK63eyuVQYbUKg
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

在PowerBI报告中显示图片，一般是通过图片的在线网址，将图片的在线地址导入到模型中，然后利用可视化来显示，参考：

[图片可视化，原来Power BI还可以这么玩](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484069766&idx=1&sn=cd86ce06b5691dfc9069923ad6028556&chksm=8e0c4f51b97bc647aacf6a2d10019e58a83e9c230d5a1f64e711facfd181ee6f5abfcf1e39e8&scene=21#wechat_redirect)

不过假如图片保存本地，并没有在线网址，也不方便发布到网络上，如何在PowerBI中显示呢？这是个常见的需求，经常有人问，这里就分享一个简易的方法。

基本思路是将图片转换为base64编码，而PowerQuery正好可以完成这种转换，以这个本地文件夹中部分国家的国旗图片为例：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPGwTviaFhXVSdC7wjOgCzcntyCEib1NNqPahT7LV32JqvFMqX4lFiccIowQXky47zAdd7gPojWCtzFg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如何在PowerBI中显示这个文件夹中的图片呢，下面是操作步骤。

**1、从文件夹获取数据**  

点击获取数据>从文件夹，选择本地文件夹路径。

导入文件夹后的效果如下。

然后可进行简单整理，这里把前两列之后的列全部删除，并把Name中的后缀删掉，提取每张图片的名称。  

**2、添加自定义列进行转换**

添加个自定义列，将\[Content\]转换为图片base64编码，M代码如下：

> "data:image/jpeg;base64, " & 
> 
> Binary.ToText(\[Content\], BinaryEncoding.Base64)

这个新列生成的字符就是每张图片的base64编码，可以将\[Content\]列删除，最终效果如下：

**3、在模型中修改编码字段的属性**

将这些数据上载到模型中，修改国旗列的属性为“图像URL”:

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPGwTviaFhXVSdC7wjOgCzcnI0IY3LtFeBic0xBRP1aGQODialtavzo3b13QvbJZr9rFiclLQI5x7jVzA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

至此转换完成，将base64编码列放进表格就可以展示出本地图片：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPGwTviaFhXVSdC7wjOgCzcnBW7QRT3M2ib9q2YWQGHHzxp5fauqweZkBR2wCmqHan21WAU8teialAAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

当然也可以用其他可显示图片的可视化类型来展示这些本地图片。

**由于PQ中一个单元格最多容纳32766个字符，而一个较大图片的base64编码通常都会超过这个限制，所以大图片一般显示不全。**

如果通过这种方式显示本地图片，最好是20k以下的小图片，比如图标、logo等更适合，大图片还是要通过在线URL的方式来展示。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你想深入学习Power BI，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和5000+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMstwXX5zrKianmFXzyqbIVgh7byfo3V8JJPmhqicywbtYkM0j2ibngnT5XBZ2AwKvGZiby9ngoKfLvzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
