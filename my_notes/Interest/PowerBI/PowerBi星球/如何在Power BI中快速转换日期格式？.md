---
create_date: 2021-10-11T22:39:22 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何在Power BI中快速转换日期格式？
source: https://mp.weixin.qq.com/s/zyzFIthle8nJxxBSjTn45w
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

今天分享一个日期格式转换的小技巧。

日常接触的数据中，你应该碰到过这样的日期格式，8位数字的日期编码：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCD0YIKEGwCpueSVD81Uu25pLXeicC7Kb4yV1FGkHM2ecZjalT9GZuI9g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来知道这是日期，但其实并不是标准的日期格式，数据分析时，系统也无法将它直接识别为日期使用，那么如何将它转换为正常的日期格式呢？

这种转换并没有难度，直观想到的做法一般是，分别提取前四位，中间两位和后两位的字符，作为年月日，再合并到一起，这样当然是可以实现的，不过还有更简单的解决办法。

**方法1：PowerQuery直接修改数据类型**

这种转换用PowerBI处理非常简单，导入到PowerQuery，首先保证该列为文本型，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDC3MfQ9ooyptzicAWFkTS1yCAMyCpjIR1JGAlzC9EQS8ibpBYqOZAhia8bQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后直接将这一列的数据类型修改为日期型，即可自动完成转换。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCyXkxwfbKsaKiaZ1ngEmxDD4jvMtSFd9ypvYdc1gZuXk85BMZ1I0hqicA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在Excel中可以同样操作快速完成转换。

**方法二：利用DAX函数：FORMAT**

上面是用PowerQuery处理的，其实用DAX进行转换也很简单，只需要用FORMAT函数就可以了。

> 日期格式 = FORMAT(\[日期\],**"0000-00-00"**)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCBnia0D2SaZKhJhCTdYqnJ5yh9F5FwAW8oqRWYfN5BdDHBEHTag1WgIg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是也很简单。  

用这种方式，首先要保证8位数字的日期列是数值型，如果是文本就先转换为数值型，才能转换成功。

并且经过FORMAT处理后的结果都是文本型，所以还要将这个新的计算列的类型更改为日期型，才能变成真正的日期列。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCcSPiaxEVYTSChdib5MbdhgwoZYic8nCMCiboW4hfplRZt4YjjtNLQXhN8A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**以上两种方法都可以快速完成转换，一般情况下，对于数据的清洗，能用PowerQuery处理的，建议先在PowerQuery中处理好，再上载到数据模型中，也就是优先使用上面的第一种方法。**  

___

另外，日常分析拿到的数据还会经常碰到一种情况，日期维度只有年月，像下面这种：

如果你需要运用时间智能函数进行灵活的分析，依然需要添加一个日期列，来与日期表建立关系。

一般可以添加一列，该年月的第一天作为日期，这就涉及到如何将年月直接转换为年月日的日期。  

这种转换，同样可以用上面两种方法，只需要在最后加上两位字符“01”，就变成了8位编码，添加方式可以用年月\*100+1的方式，比如202108乘以100，再加上1，就变成了20210801。

如果用FORMAT，直接这样写，就可以完成转换：

> 日期列 = FORMAT(\[年月\]\*100+1,"0000-00-00")

对于已经转换为日期格式的日期，假如想让它显示为其他的形式，比如月份、星期几，也都可以利用FORMAT函数来完成，只需要灵活使用它的第二个参数就可以了：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCia8U3o3TyanvQ4AfiaK2cMEmd2BVZEVibVP5CTWzaDnJFa7FPGK9rmOAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

更多FORMAT函数的用法，参考：[利用FORMAT函数自定义数据格式](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067980&idx=1&sn=4c314be995c216a5a6e6f7a49886cc2f&chksm=8e0c745bb97bfd4d1092fadd56e335ccb0d27f38cffeca7d234fef18eaae81da052c7c69900e&scene=21#wechat_redirect)

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN6oGnIQSa3kx3M0QQESdrYCTV9SBx5LXD4kp3icA9LouW3YN2z2njBWWQzM1zia9Fbeky0fdIpNakw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和3800+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMqicSUp5EfHiae4ibtEjIZsDCy5RUEz1Yp2hsG1ExlG3XiaqfWPqspJ1oiaEcKjuJCKPStBaWQXO6SOew/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
