---
create_date: 2022-12-25T00:08:52 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI表达羊
source: https://mp.weixin.qq.com/s/qFI0mkBfgvDyTSOeLJgf-Q
author: wujunmin
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

2022年12月，新冠疫情进入新的阶段，愿诸君安康。最近常用的问候语成了：你羊过了没？

微信的疫情动态一些模块也悄然下线。以下是微信之前的新增阳图表，有两个特点：条形是渐变的且末尾有人物图标。这个图表不再有用，但可以参考其展示方式。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6TcNWyxxEWcENibcZ7XTSLrxWibPK4gQgWMozHibVWfCPWH02fxzlNwjQ0H2cfxx5tPjedMV4qOTdeNA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

人像图标可以在PPT找到，颜色调整为红色，然后用黄老师的工具转换成base64（[一键解决PowerBI本地图片显示问题](http://mp.weixin.qq.com/s?__biz=MzI1OTA5NzU3Mw==&mid=2247483832&idx=1&sn=020c3bc640451cc02369a703ed775531&chksm=ea7f5732dd08de24ea119bec9478bd705b86067ad58993bec5fe100d64ee558418c116104da1&scene=21#wechat_redirect)），在网上找个类似的图片链接也可以。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TcNWyxxEWcENibcZ7XTSLrxnTMc0aWsURaXiaEJXQrO6vXeDAibe7mfAE9Otxk5eiagK0d4PlJPu3WYA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

虚拟数据如下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TcNWyxxEWcENibcZ7XTSLrxkBDRm59mGpRfKF9MRh0zGhDIeTrdBaG31uibaibT6ibpYQrydTcxhzV0A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

新建度量值：

```
条形图 = 
```

度量值中，rect生成条形，第一个text生成类别标签，第二个text生成数据标签，image生成人物图标，color变量产生渐变效果。将度量值放入HTML Content这个视觉对象，设计即完成。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TcNWyxxEWcENibcZ7XTSLrxezGmAahR6fo6Vbo0ulgB0AVHqZH6b5xw0Hz5BSHtmxCcz7Q8u0YDsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

动画演示：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/JHQQIBqYy6TcNWyxxEWcENibcZ7XTSLrxFwtBOiaSEIZwXOvO9twMoOlCRkwSFP5SibZFARPRhBoHBt1Me2OWfFbQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

本文PBIX源文件在下方知识星球下载。直达链接（左下角阅读原文也可访问）：_https://t.zsxq.com/09NG48LbQ_

星球将在2023年1月1日涨价，有兴趣的读者不要错过。详细介绍：[Power BI业务实战及图表开发社群&视频课程](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491267&idx=1&sn=9f8011a4c2a7f38f17b6ef4168625c63&chksm=97db2793a0acae853c07277e58d55c0b8db67e953b44228508b7282f4e907af330cf64efbf51&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6SrFOpSISmqT2k74QM76UrbIBKw9vBMzBUmBfibKCas2iccpABJdicQ4UNYGL2QCMLGaesXVyJ601kvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
