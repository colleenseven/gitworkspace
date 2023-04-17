---
create_date: 2022-12-13T00:11:08 (UTC +08:00)
tags: wx/pbi/可视化图表 
aliases: null
pagetitle: Power BI模拟谷歌2022搜索排行榜
source: https://mp.weixin.qq.com/s/UhQvxhD9GarPtpqGeKLntw
author: wujunmin
status: 已完成 
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

谷歌近日发布了2022搜索排行榜，以下是statista制作的美国榜单图表。这个图表有2个主要特点：第一名带有半透明背景色，且右侧有个搜索图标。Power BI如何模拟这样的表格？

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6QyfSSUA5whbyseLlV8gibwFMrCGdCnYjHhueEy2afT5FtjnkU9bl4DUNfiaQsfIl3Pd7ZPtPoiadvOQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**首先，半透明背景色如何实现？**以上图左上角的榜单为例。
![https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QyfSSUA5whbyseLlV8gibwFTNln5ww80BrV9FSVeXZAYibGCUyAKmplOKlp9QtFZTZgAGItwgcSe0w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QyfSSUA5whbyseLlV8gibwFTNln5ww80BrV9FSVeXZAYibGCUyAKmplOKlp9QtFZTZgAGItwgcSe0w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

新建一个背景色度量值，rgba前三位表示颜色，最后一位表示透明度，透明度设置为0表示完全透明。这里我们设置了一个有一定透明程度的蓝色。

```
背景色 = 
IF ( SELECTEDVALUE ( Searches[Index] ) = 1, "rgba(0,0,255,0.2)", BLANK () )
```

拖拽一个表格，放入searchers字段，为该字段的背景色条件格式引用上方的度量值，即完成设置。
![https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QyfSSUA5whbyseLlV8gibwF3TXGkvicNib6PG1cJd1v28DTA651l4IYA8nIcnz5T6hic7tFVlAVibQbmg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QyfSSUA5whbyseLlV8gibwF3TXGkvicNib6PG1cJd1v28DTA651l4IYA8nIcnz5T6hic7tFVlAVibQbmg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
**其次，搜索图标如何设置？**可以想到使用条件格式图标。但是Power BI内置图标并无此项目。所以需要制造一个，第一种方式是利用emoji表情包，搜索可以得到表情包放大镜的emoji的代码。  
![https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QyfSSUA5whbyseLlV8gibwFZ4zvvickkY2icO5QnAjl4STZ3kWO48kFYA037xSNN8Ch9Gd7tN5YgUpw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QyfSSUA5whbyseLlV8gibwFZ4zvvickkY2icO5QnAjl4STZ3kWO48kFYA037xSNN8Ch9Gd7tN5YgUpw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
表情包无法直接放入条件格式图标，需要使用SVG图形包装起来，参考：

[如何在Power BI使用表情包](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488916&idx=1&sn=b120f3fe9cfb25464b71cf83db88ba6a&chksm=97db2cc4a0aca5d26da359217fd947d1f41e385ed133616fd6b3e49968e975ef626a1a155c4a&scene=21#wechat_redirect)，度量值如下：  

```
放大镜图标-emoji = 
VAR emoji=
"data:image/svg+xml;utf8,"&"
<svg xmlns='http://www.w3.org/2000/svg' height='100' width='100'>
    <text x='0' y='80' font-size='80' text-anchor='start'>"
        & UNICHAR(128269) & "
    </text>
</svg> " 
RETURN
    IF(SELECTEDVALUE(Searches[Index])=1, emoji, BLANK())
```

这样，我们得到了以下效果：  
![https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6SRPYVqGPjQ3havHppsYwpM6R5W5ZauSLKsoyqYv0F49LObqNduJdN2peQrjcI5fANPljeicpwhibCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6SRPYVqGPjQ3havHppsYwpM6R5W5ZauSLKsoyqYv0F49LObqNduJdN2peQrjcI5fANPljeicpwhibCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
搜索图标看上去和statista的有些不一样，不同浏览器、不同设备对相同表情包的显示会有差异。这个时候，不妨考虑纯SVG构建的图标：

```
放大镜图标-SVG = 
VAR SVG = 
"data:image/svg+xml;utf8,
<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32' stroke='Grey' stroke-width='2'>
    <circle cx='14' cy='14' r='12' fill='none'/>
    <path d='m23 23 7 7'/>
</svg>" 
RETURN
    IF(SELECTEDVALUE(Searches[Index])=1, SVG, BLANK())
```

显示效果如下图所示，是不是又接近了一些？  
![https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6SRPYVqGPjQ3havHppsYwpMLRdSGyS0mz98u3x0l3l6fiaH7PrPkibf7T5VSyjuRmQrYpYPbrJfTpvQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6SRPYVqGPjQ3havHppsYwpMLRdSGyS0mz98u3x0l3l6fiaH7PrPkibf7T5VSyjuRmQrYpYPbrJfTpvQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
还有读者可能会问，这和statista的还是不一样呀，背景色没有边框。非常遗憾，Power BI原生表格暂时无力这么操作。完全相同的效果只能文本、背景色、搜索框全部使用SVG生成了，且使用第三方视觉对象显示。下图左上为emoji图标方式，右上为SVG图标方式，下方为所有元素SVG方式。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6SRPYVqGPjQ3havHppsYwpMKQrrZka958ibIka1CYhp0gZfvGxZECoI3vbWAmK4LzRicxhuuXySebtA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

本文配套pbix文件在下方知识星球下载，直达链接（可左下角阅读原文）：

_https://t.zsxq.com/09983UYv8_

