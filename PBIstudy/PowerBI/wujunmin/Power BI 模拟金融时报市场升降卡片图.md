---
create_date: 2023-01-09T00:05:55 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 模拟金融时报市场升降卡片图
source: https://mp.weixin.qq.com/s/oSOZAXj6xLZMD_4mjFQzLQ
author: wujunmin
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

在金融时报的市场数据模块看到如下卡片图，上升和下降使用不同方向的五边形表示，数据的位置也随正负数变化而上下进行调整。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Q4VHAXAicFgHMyjj9xq1OSbvnD4WXbGJs6AUEMYCXyWZOtMHSnfHwyHVxGzibiaAdGmSvCSgicYkY5qw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Power BI表格模拟效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6Q4VHAXAicFgHMyjj9xq1OSbh5naeKlHn1M8ibveLdYzQ82WHsxLg77hUOoyKicIMaKrxqiaX1t0NFrJQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

原理是使用SVG矢量图生成五边形和文本，度量值如下，将度量值标记为图像URL拖入表格即可显示，度量值中的Value替换为你的指标进行复用。

```
模拟金融时报升降卡片 = 
```

本文pbix文件在下方知识星球下载，直达链接：

_https://t.zsxq.com/09QEBVHUU_

更多模拟大厂图表参考：

[Power BI模拟大厂图表总结贴-2022版](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491403&idx=1&sn=b868c0fc4b935aaba5f3490533cfb5c9&chksm=97db261ba0acaf0d717007b39c83e1dfa5a6a995bc1abaf778faa15981ec11139a4fd8b291b6&scene=21#wechat_redirect)  

___

  
加入知识星球，享有90+节视频课程，200+源文件，详情介绍：[Power BI业务实战及图表开发社群&视频课程](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491555&idx=1&sn=938fc2d95536402d9eddf5bf45e2a3a1&chksm=97db26b3a0acafa5e88ff6afe782031937a6023e5c46ea6e04e64c76dfc699963b302a978d7f&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6SrFOpSISmqT2k74QM76UrbIBKw9vBMzBUmBfibKCas2iccpABJdicQ4UNYGL2QCMLGaesXVyJ601kvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
