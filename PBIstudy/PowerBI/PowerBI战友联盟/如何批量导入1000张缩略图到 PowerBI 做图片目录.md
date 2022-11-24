---
create_date: 2022-06-13T12:43:18 (UTC +08:00)
tags: 
aliases: null
pagetitle: 如何批量导入1000张缩略图到 PowerBI 做图片目录
source: https://mp.weixin.qq.com/s/241U2tYOYHAM2cn3wF9_Mg
author: BI佐罗
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月13日 20:00 直播

PowerBI

视频号

小伙伴问，有一个产品列表以及对应的 1000 张产品图片，现在的问题是：

-   如何构建产品列表
    
-   可以容纳 1000 张图片
    
-   无需网络
    

大家都知道 Power BI 可以显示网络的图片，只需要设置好路径即可。

但有的时候，我们不希望企业内部的图片暴露在网络中，最好可以内置在 Power BI 中，这可以实现吗？

由于图片占有一定的体积，这里的需求恰好是：图片不要求大图，只需要可以快速浏览项目列表。

## 缩略图的生成

先预先准备好 1000 张产品图片，例如：

用任何一个图片浏览工具或看图工具都可以批量压缩图片。

例如这里用了 2345 看图王，压缩如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM8j1KUCLtxuiakZdIse76mgTHXEu5iaAxIoy1JJt9XwX5ib3hZUicTBPD1jia7u6EpNRpJjZR1yNmoLTA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

> 💡注意
> 
> 2345 看图王可能有广告，这里仅仅做一个示范，批量处理图片的工具有很多，并非本文重点。

处理完成后，就有了 1000 张缩略图小图片。如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM8j1KUCLtxuiakZdIse76mgDJzlDAdNnLA3t4kpjbT9mvtldSy1bejTtQTqL9baW8vCbDKia8zlTfw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

接下来，就是如何将图片转为文本格式来存放。

## Power Query 自动转换

既然 Power BI 可以显示 BASE64 格式编码的图片，那么可以在 PQ 中完成转换，方法如下：

首先用 PQ 获取文件列表，然后进行自定义列的转换，如下：

```
"data:image/png;base64," & Binary.ToText([Content])
```

着非常简单，仅仅将字符串进行拼接以满足 BASE64 格式图片的要求。

## 显示图片列表

将这些数据加载到 Power BI 的数据模型中，对此构建度量值如下：

```
Image.Mini = SELECTEDVALUE( 'mini-images'[ImageText] )
```

并设置该度量值的属性为：图像 URL。

将图片的名称和该度量值放入表格得到：

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LM8j1KUCLtxuiakZdIse76mgwuCQe1ibnzKzrQiaur9Ngn4uoGnGPia2QfZ3LYhq1q4g5qn8js6vxJtug/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这就是我们需要的结果。

没有依赖于网络环境，仅仅通过 Power BI 和本地图片列表就构建完成。

## 总结

这个技巧的好处在于：

对于大量小图片的情况，完全不需要网络，可以完全使用 Power BI 内置完成，且实测速度非常快。

这是构建产品 SKU 导览等业务需求的高效安全的解决方案。

![](https://wx.qlogo.cn/finderhead/Q3auHgzwzM4Rz9mYvEFH2tuPTpv0svaghGlMxxNNbNjkwBJCRr1RFw/0)

**PowerBIMBA**

，

06月13日 20:00 直播

PowerBI

视频号

在订阅了BI佐罗讲授的《BI真经》之《BI进行时》课程区，除了可以下载本文案例，还可以观看视频讲解。

**Power BI 终极系列课程《BI真经》**

[

BI真经 - 让数据真正成为你的力量





](http://mp.weixin.qq.com/s?__biz=MzI1MDA4MzcxMA==&mid=2650788512&idx=1&sn=76972ff4b0cf265fe9479c6457b04b47&chksm=f18cd2b1c6fb5ba7386eb0bb835280bd8a651bfe0481cc78f20fc30b80c60d2d4cb7eb5b1e3e&scene=21#wechat_redirect)

扫码与精英一起讨论 Power BI，验证码：data2022

![图片](https://mmbiz.qpic.cn/mmbiz_png/09hv4Xua0LOiad5BOrdQTKpB733esKiaxZa53LXWIPlQicMjxntaRr3a2hnMmuibTib8QacXeiakucDr7lSNGkuV2MXw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“阅读原文”进入学习中心

**↙**
