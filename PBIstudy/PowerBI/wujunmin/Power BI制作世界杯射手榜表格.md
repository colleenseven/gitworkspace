---
create_date: 2022-12-16T00:10:30 (UTC +08:00)
tags: wx/pbi/可视化图表 
aliases: null
pagetitle: Power BI制作世界杯射手榜表格
source: https://mp.weixin.qq.com/s/NG_geLZdbkraQNwYA30omA
author: wujunmin
status: 已完成 
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

前期有关世界杯的文章：

[_Power BI足球风格条形图_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491136&idx=1&sn=cd0c9a60c8009f660315298339ba8ef1&chksm=97db2710a0acae06e20fe5cd26ba6e8ccb89c5955ce3ba2fbf922d842c2c0229711d676c8cda&scene=21#wechat_redirect)  

[_这份超详细的足球数据值得拥有_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491208&idx=1&sn=985b4c304ebedcee00f265b54483f9ee&chksm=97db27d8a0acaece6f9c32d3eb93ebc91d425ac5d259b62f24d2da03c8f3095e225550ceecf3&scene=21#wechat_redirect)

[_世界杯可视化作品：阿根廷对克罗地亚_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491303&idx=1&sn=18daa2aa7730ec79825f8cec1ed6832a&chksm=97db27b7a0acaea1168313a7e3dea733b038a2f256ec4c6b6bdaca4dbeeae2425d4bed5bb1a4&scene=21#wechat_redirect)

下图是腾讯体育的世界杯射手榜，这个表格的特点是带有球员头像，进球括号标注了点球数量。这里介绍两种Power BI的实现方式。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6Shbs94bkNUpvk4IMvTbSAxj9xQibGiajnQF9udYtPawUUp9UaJVcURxSmeLkVwPNibVUfcU7yBeARcw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

射手榜的实时数据可以在腾讯体育或者CCTV官网获得，以下是链接：  

_https://sports.qq.com/kbsweb/qb/rank-tab.htm#/4/leaders/61_

_https://worldcup.cctv.com/2022/scorers/index.shtml_

Power Query可以直接导入数据，导入后如下图所示：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Shbs94bkNUpvk4IMvTbSAx7QCQJetLaxCsdWob2oItpmH3O1Yb6lYxJ9yib7TDm6xc3yLlAznGkBA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将头像（标记为图像URL）、球员、球队字段放入表格，新建进球和点球合并的度量值，也放入表格。

```
进球（含点球） = [进球数] & IF( [点球数]>0 , "(" & [点球数] & ")" )
```

显示效果如下图所示：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Shbs94bkNUpvk4IMvTbSAxsibS4f1JdDTfia4ciaVST1OeQIiaA72IOibUjrgR367dkBHPbshVI3XPvoQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

头像的高度可以在下方位置调整：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Shbs94bkNUpvk4IMvTbSAx1t61MLhgJ5v6zXj5sbuoZPrlMkQm5yn5ickkS1PZFZiaOjJkrtqDtyVA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种方式进球数是一个文本，无法降序排列，这里可以利用条件格式对总进球和点球进行拆分。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Shbs94bkNUpvk4IMvTbSAxOIn5KiaOJTfm6CfeiaO5IYMgYeib7zxIoZKPd5g5ibHqOvVgsAiaicwprwzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

表格仅仅拖拽三个字段，但是显示五列数据，不在表格列的数据为头像和点球数。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Shbs94bkNUpvk4IMvTbSAxKjvR2hSqfGassfFu8YH2vudWlYiagm0hJp3u8sX8u0POvqA7jaIDUibw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

头像显示时，可以对球员字段施加条件格式图标，图标为头像列，如下图所示：  
![https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Shbs94bkNUpvk4IMvTbSAxkPhIBIpJo02mt6LQ1WRvauZXxA79L7xZUXUSXHSsWw0k5k2kZcjRvg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Shbs94bkNUpvk4IMvTbSAxkPhIBIpJo02mt6LQ1WRvauZXxA79L7xZUXUSXHSsWw0k5k2kZcjRvg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
点球显示时，可以将点球数据包装成SVG矢量图图标（Power BI不支持纯文本类型的条件格式图标），点球图标如下：  

```
点球图标 = 
VAR SVG= 
"data:image/svg+xml;utf8,"&"
<svg xmlns='http://www.w3.org/2000/svg' height='100' width='100'>
<text x='0' y='55' font-size='70' text-anchor='start' dominant-baseline='middle' font-family='Segoe UI'>("
        & [点球数] & ")
</text>
</svg> " 
RETURN
IF([点球数]>0,SVG)
```

将该度量值施加于进球度量值，并放在右侧，产生进球点球一体化显示的效果。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Shbs94bkNUpvk4IMvTbSAxHhSrWrf0nyp3gn60RN7H2Dnco9Rvb5bOcflYGfpLuDwjGKicSjg1mng/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个表格还可以进一步优化，球队名称前加上国家/地区的旗帜，旗帜和点球一样，使用SVG条件格式图标，图标可以参考本文下载：  

[世界杯可视化之国家地区旗帜](http://mp.weixin.qq.com/s?__biz=MzI1OTA5NzU3Mw==&mid=2247485615&idx=1&sn=1824173a5dfa2e529ce239aeb2ca8907&chksm=ea7f5e25dd08d733771567823036c1bb7f2291922353bb3539124ccff764f3ade26d2d247faa&scene=21#wechat_redirect)  

以上。
