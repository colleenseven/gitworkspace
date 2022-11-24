---
create_date: 2021-09-16T22:41:54 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI可视化技巧：突出标识特定事件的数据
source: https://mp.weixin.qq.com/s/xy4x5X_efKF8kppzr_c2Xg
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

上一篇文章介绍了突出显示某一个期间的数据，是通过切片器来选择一个特定的期间，参考：[PowerBI可视化技巧：突出显示特定期间数据](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077392&idx=1&sn=22aa0f16e9929482ac17fa48ef7be48a&chksm=8e13a987b9642091786b45ecb7ac8515495e03c54bbf7dcd73a2c1f3f8854fa7794872db1576&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNVwQ5v1HFlE7tAqETZfQqPqEzIgMmEZG6FXicgpU6QAFeSbcQEERqWhnDNxsvjm5x1I6iaygq31JhQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

很多情况下，我们并不会随意查看某个时间段，而更关注某一个事件的影响，只需要突出显示该事件发生期间的数据即可。

假如其中有两次节日促销活动，把这两次活动的起止日期制作一个事件表，导入到PowerBI中：

那么如何突出显示这两个时间段内的数据呢?  

其中一种方式，就是按照上篇文章的做法，将X轴恒线的开始和结束点分别用这两个度量值确定：  

> 开始 = MAX('事件表'\[开始日期\])
> 
> 结束 = MAX('事件表'\[结束日期\])

然后用事件作为切片器，就可以动态切换某个事件发生期间的数据：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNEN8FA7pbHbBA2Yz9K6ibiaUhTibDyHr9DGVgvHu1rs8c0IxOJWB4dXXoWcEFSj56FuicUGmoPF1bbZg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

其中右上角的指标计算的是该期间的总销售额，是靠这个度量值计算的：

> 本期间总销售额 =
> 
> CALCULATE(
> 
>     \[销售额\],
> 
>     TREATAS(
> 
>         CALENDAR(\[开始\],\[结束\]),
> 
>         '日期表'\[日期\]
> 
>     )
> 
> )

上面的效果是利用X轴恒线的功能实现的，虽然可以突出显示某一个事件，但无法同时突出显示两个期间。

下面介绍另一种更常见的做法，只需要先写两个度量值：

```
销售额 事件发生期间 = 
```

```
销售额 非事件发生期间 = 
```

**第一个度量值判断当前上下文的日期是否在事件表的某一个事件中起止期间内，如果是，则返回销销售额；另一个度量值的逻辑则正好相反，如果不在任何一个事件的起止期间内，才返回销售额。**  

用日期表中的日期作为轴，这两个度量值作为值生成堆积柱形图，为两个值设置不同的颜色就可以了：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJNEN8FA7pbHbBA2Yz9K6ibiaUutmzbm5yXkGYcyTKjWhibj9ZKraibQIuYmhDShN0rld7HXZsMrib0qQAw/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

它可以同时标识出多个事件的数据。

右上角的合计销售额是这样写的，

> 销售额合计 事件 =
> 
> SUMX(
> 
>     VALUES('日期表'\[日期\]),
> 
>     \[销售额 事件发生期间\]
> 
> )

这个度量值迭代上下文的所有日期，先计算每一个日期的事件销售额，由于在非时间发生期间，事件销售额都等于0，所以最终的结果就是将所选事件发生期间的数据全部累加起来了。  

第二种做法主要是利用DAX实现的，和辅助线的功能无关，适用性更强。

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkvUibMVjf4z1bY0MYFh7lAkqrcHiaEHE4UicvjJjibpmkxJjc4TDlVO04qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OyUpTibBJjoq1jk8CzVZJz6s4nJRW1ViammT4ecqAJ7iapDccKNNrwtLYQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077212&idx=1&sn=bb3dac9becf80b5d929e5dc8405158dd&chksm=8e13a84bb964215d6362f78768cdefa18def4dfc8cd5c14f075442431604ed9c9729e4051a4b&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkNI6YYicVJ3RPhufJhoh3lzY1e1dgUyxy6yGkk4UvZcuTfVGTc89iaI3Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJP8Cvmfx7v8oUqdoQaMmuDAG2GibhzIydz7aGIyMr9drbJx6vevzfXib5D6NFtuR4Qu3TVQibQRqrVWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484072351&idx=1&sn=fabb08c54790ac1225b470fd647c7a5e&chksm=8e0c4548b97bcc5e0450f1945a2c76039bbb42650bcb1edbc856820836d63d32af4c7780e31a&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和 3k+ 学习者一起成长
