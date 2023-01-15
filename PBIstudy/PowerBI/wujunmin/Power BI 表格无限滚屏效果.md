---
create_date: 2022-12-02T00:12:28 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 表格无限滚屏效果
source: https://mp.weixin.qq.com/s/zmyoZUDtuEmFT44sMtBdSA
author: wujunmin
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

前期滚屏相关文章  

[_PowerBI无限滚屏__基础篇_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247490409&idx=1&sn=8abcabc9baac245b0860db54394586c6&chksm=97db2239a0acab2fc09ff376ca93df96c2a2ec75976e2490e4b622c605a1d4e08236a674d3cd&scene=21#wechat_redirect)  

[_Power BI滚屏实战：人员业绩达成滚动播放_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247490601&idx=1&sn=03399c57bfef47a5ded85f2f9441e743&chksm=97db2579a0acac6f2de7eaa5520ddedfe7a45ee3fced0ecad6ae6a62ce95baebd2806ec0c37b&scene=21#wechat_redirect)  

[_Power BI滚屏实战：多地图滚动轮播_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247490689&idx=1&sn=baeac1cca8aa6883bfd70d9e0cb87136&chksm=97db25d1a0acacc721f5198a80efb0bce0306f9c2c5a808dac8814e408ef2dc5d8ade20fe02a&scene=21#wechat_redirect)  

[_Power BI、黑客帝国、苏东坡和老子_](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247487371&idx=1&sn=273d121509077b50d2764f25f8aa199f&chksm=97db36dba0acbfcdd46713d5784edf752b4810307c52232473c7d5da70a14275a6d5f3122f55&scene=21#wechat_redirect)  

表格的滚动播放可见于机场、火车站的车次播报，医院门诊大厅的科室候诊播放，也可用来解决其它业务中的表格过长、显示不全问题。  

以上链接文章讲过几种形式的滚屏，表格滚动起来其实没有什么不同。以下是借助HTML Content视觉对象展示的滚屏效果。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/JHQQIBqYy6Qic2BjZBcfAeE1n9NFG0s0NKuJ75Mn7tGe5DibZ4URLwibdn8AYEP9tzWuGQxeQ9h9aMUHW7tF9FQ5g/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

把表格内容用SVG的text包起来，下方度量值列举了三个字段，实际可用任意个，X的值决定了不同字段的显示位置。  

```
SVG滚动文字_HC版_向上 = 
```

把以上度量值放入HTML Content的Value显示，默认显示三行，如想调整，则变更viewbox的值。  

那么原生表格可用实现这样的效果吗？也是可以的。  

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

原理和上方的度量值区别不大，有些细节需要注意：  

1\. 表格矩阵需要为每个字段新建一个独立的动画度量值，且标记为图像URL，下图是5个动画度量值。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

2\. 度量值要在SVG前加上识别符：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Qic2BjZBcfAeE1n9NFG0s0NTHqJxPRlhxuicHic3UBlv9pLTEOMKt36vlWRDiafDCIPUqUae4ns0VkMg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

3\. 如果在表格同一行显示多行数据，照搬上方HTML Content的度量值即可，如果想要显示的行数更多，则需新建一个索引列，按索引大小显示。

详细的视频教程及pbix文件下方知识星球观看和下载。直达链接（也可左下角阅读原文访问）：  

_https://t.zsxq.com/08V2L4P5c_

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QcN06GNG2hRD8asNgnfgFxNftZAD1gAiaPUW7LBbmKElZXHic6NGBILDSYpZustlBQibqPVwTlFItaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6SrFOpSISmqT2k74QM76UrbIBKw9vBMzBUmBfibKCas2iccpABJdicQ4UNYGL2QCMLGaesXVyJ601kvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

[详细介绍](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491183&idx=2&sn=17f974151d497c33806a9c0a0ed2c198&chksm=97db273fa0acae29dd8fae2bbf270ca262049d5f3044a10d1e746021790d110fd597d0faa422&scene=21#wechat_redirect)
