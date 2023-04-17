---
create_date: 2022-12-28T00:08:26 (UTC +08:00)
tags: wx/pbi/可视化图表 
aliases: null
pagetitle: Power BI表格显示图片的若干问题
source: https://mp.weixin.qq.com/s/WQL2fIKFg8n44SQ_DHblSg
author: wujunmin
status: 已完成 
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

**为什么要在表格存放图片？**

可能为了展示人物、产品照片；可能为了展示图表；可能为了美观……  

**Power BI表格可以存放什么形式的图片？**  

jpg、png等常见格式的URL，SVG编码，本地照片转BASE64编码。URL通常表现为：

```
"https://wujunmin.png"
```

SVG表现为：  

```
<svg viewbox='0 0 6 12' xmlns='http://www.w3.org/2000/svg'>
```

BASE64表现为：

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6R2qHRRkS7iaEOFbkicreBHoOb0fWxxl8L0Jx3Fq0WP1IzamjHE0g66PdpLzxgcKjknat7z0af8E6Fw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**不同形式的图片应用场景是什么？**  

==URL常用来装饰或显示宜对外公开的图片信息；SVG常用来装饰或自定义个性化迷你图；BASE64适用于不想使用网络图床的情景。  ==

**图片在表格怎么显示？**

有两种方式，直接在表格列显示或者条件格式图标显示。在表格列显示时需要将图片列或者图片度量值标记为图像URL，在条件格式显示时不需要标记。针对SVG表格显示，无论直接显示还是条件格式，均需要在SVG代码前加上

data:image/svg+xml;utf8,

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TkfVmjp4rKe6UPjWK6ickPM5y9p0DeDicBlXj0qAOBM4c46FqiaECumE78vEbbkadxFBhoN3HhrQAhQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

下图左侧是PNG图片URL，右侧是SVG：

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TkfVmjp4rKe6UPjWK6ickPMobpRiamKgAJFgH6O5NwDLHAFB0BQLVqb175xMo6PdegibNfiaxzBOZ0zQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**图片哪里可以获得？**

公司内部的产品、人物图片当然内部获得。装饰用的PNG图片和SVG图片推荐以下三个资源：  

_https://pngimg.com/_

_https://www.iconfont.cn/_

_https://iconpark.oceanengine.com/home_

本地图片转BASE64参考此视频推荐的转换工具：[Power BI 批量导入本地产品、人物照片](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247490046&idx=1&sn=f399c968180d24318b7abed5a1f206f5&chksm=97db20aea0aca9b86ef50d3504ebc68b5c1ea2b2102868752339963fda2ff7f2d1b1a8d26e42&scene=21#wechat_redirect)

SVG自定义表格迷你图表本公众号已经分享过很多篇了，读者可以翻看或加入知识星球深度学习（[Power BI业务实战及图表开发社群&视频课程](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491267&idx=1&sn=9f8011a4c2a7f38f17b6ef4168625c63&chksm=97db2793a0acae853c07277e58d55c0b8db67e953b44228508b7282f4e907af330cf64efbf51&scene=21#wechat_redirect)）

**表格显示图片的限制是什么？**

在表格显示时，最大限制有两个：首先是只能是正方形的空间（并不意味着只能显示正方形的图片），格式设置时只能设置高度可以看出；其次最大图像高度只能150个像素。在条件格式显示空间也只能是很小的一个正方形。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6R2qHRRkS7iaEOFbkicreBHoO08WLESkKicLyxZ80BNKcps4Y6L2RHzBq0mK4b3jKFRbHoujVCia1ibcYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

尽管局限明显，也可以戴着镣铐跳舞，发挥很多创意。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6R2qHRRkS7iaEOFbkicreBHoOic63trG7oH4BGkCHJgEZTTsyGqIiaEvk560q5S5mzQGNnp1LSZJXPbhQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6R2qHRRkS7iaEOFbkicreBHoOJPribjuHOmQOib6xWWw8blMt74CS5rg6UzicoRQ0PmCvnZxzLrkFEnc2g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6R2qHRRkS7iaEOFbkicreBHoO5fMBhqt53KsL28w3FyMLJrEbhIYFBxViazlEiaF2Ruic9cnuibDuTVsUuA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**如何突破限制？**  

例如在自定义图表时，条形图需要很大的长宽比，但表格有图片正方形限制，下文的技巧进行了突破尝试：[Power BI原生图表自定义填充图案](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491163&idx=1&sn=ff7b4bcb76fac28722d51b8c0b37132f&chksm=97db270ba0acae1d5190a32272b5a70639c79e8c56be4577d9d0b864dec89ca3b4f313ab2425&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6R2qHRRkS7iaEOFbkicreBHoO2h6mNBIaoYrzLoDmUAJ8TdSOPHjY0ibiahR266QuesocxnCZBTOvia2uA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上方是横向联动，也可以纵向联动：[Power BI窗口函数应用于图表设计](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491348&idx=1&sn=d457df1d8a24ed4d83b5b1bc2f25516c&chksm=97db2644a0acaf52ba7a522ead1495e18e7d370b39beeb463660e81239a50645fbc92dec833a&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6R2qHRRkS7iaEOFbkicreBHoOE9TdEgoD7Og7nURIiaBxhZO9I3nwPLuLooxo3QtYgn0WPxDhlc6GfyQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

完。  
