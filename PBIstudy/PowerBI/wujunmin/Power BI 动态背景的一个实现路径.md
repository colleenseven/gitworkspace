---
create_date: 2022-12-06T00:12:07 (UTC +08:00)
tags: 
aliases: null
pagetitle: Power BI 动态背景的一个实现路径
source: https://mp.weixin.qq.com/s/E6HZ0gPKCoaLqeEstzFKgg
author: wujunmin
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

已知Power BI可以插入GIF格式图片充当动态背景，然而寻找合适的GIF是困难的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6QFTVHVaEzwMsbc5m3AMrdYBtU96wJ4aFHWj5Bxek8tkfuG0vpGgNVhBIeoN9tKhay1iaU3XMmjjZQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

高清的短视频却是很容易找到，把视频转换为GIF是一个不错的方法。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/JHQQIBqYy6QFTVHVaEzwMsbc5m3AMrdYnUXg8Jb7cqWbzqZdJa3ZXsk9O2C1k65DljDAjOZerzfF0ymNDBGTvQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

以旋转地球为例，在https://pixabay.com/zh搜索地球，可以找到近千种地球短视频，选择喜欢的免费下载，建议时长在30秒以内。

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

接着在以下网址实现视频转GIF，约几十秒后可以得到GIF文件，转换时注意帧率不宜过高，同时可以使用该网址的压缩功能缩小GIF体积。

_https://imagestool.com/zh\_CN/video-to-gif.html_

![图片](data:image/svg+xml,%3C%3Fxml version='1.0' encoding='UTF-8'%3F%3E%3Csvg width='1px' height='1px' viewBox='0 0 1 1' version='1.1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg stroke='none' stroke-width='1' fill='none' fill-rule='evenodd' fill-opacity='0'%3E%3Cg transform='translate(-249.000000, -126.000000)' fill='%23FFFFFF'%3E%3Crect x='249' y='126' width='1' height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

___

《**Power BI业务实战及图表开发**》知识星球，左手业务、右手技术，一方面分享Power BI零售业务实战视频课程及本公众号发布的实战案例源文件，另一方面致力于使用DAX低代码个性化制图，摆脱内置图表和第三方图表限制。

星球已发布超过70节视频课程，100+公众号源文件。详情介绍：[Power BI业务实战及图表开发社群&视频课程](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491183&idx=2&sn=17f974151d497c33806a9c0a0ed2c198&chksm=97db273fa0acae29dd8fae2bbf270ca262049d5f3044a10d1e746021790d110fd597d0faa422&scene=21#wechat_redirect)

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6SrFOpSISmqT2k74QM76UrbIBKw9vBMzBUmBfibKCas2iccpABJdicQ4UNYGL2QCMLGaesXVyJ601kvw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

欢迎零售业同仁、Power BI和Excel用户扫码或左下角阅读原文加入星球，星球将在2023年1月1日开始有一定幅度涨价，现在加入即是最优惠。
