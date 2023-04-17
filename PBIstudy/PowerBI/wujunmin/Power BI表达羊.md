---
create_date: 2022-12-25T00:08:52 (UTC +08:00)
tags: wx/pbi/可视化图表 
aliases: null
pagetitle: Power BI表达羊
source: https://mp.weixin.qq.com/s/qFI0mkBfgvDyTSOeLJgf-Q
author: wujunmin
status: 已完成 
category: 浏览文章 
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
VAR MaxValue =
    MAXX ( ALLSELECTED('表'[地区]), [新增]) 
VAR Color= "
    <defs>
        <LinearGradient id='w'>
            <Stop offset='0%' style='stop-color:Snow'/>
            <Stop offset='100%' style='stop-color:tomato'/>
        </LinearGradient>
    </defs>"
VAR Chart ="
    <rect x='20'  width='" & 100 * [新增] / MaxValue & "' height='12' fill='url(#w)' />
    <text x='0' y='8'  text-anchor='start' font-size='6' >" & SELECTEDVALUE('表'[地区]) & "</text>
    <text x='" & 24+100 * [新增] / MaxValue & "' y='8'  text-anchor='start' font-size='6' >"
                &  [新增] & "</text>
    <image xlink:href='data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciPjxwYXRoIGQ9Ik00LjA5IDEuMDY0YTEuMDkgMS4wNjcgMCAxIDEtMi4xOCAwIDEuMDkgMS4wNjcgMCAwIDEgMi4xOCAwem0xLjg4MyA1LjQ5NGwtLjc2NC0zLjE3NGEuNjMuNjMgMCAwIDAtLjE2NC0uMjkzQTMuMzA4IDMuMzA4IDAgMCAwIDMuOSAyLjUwNGMtLjMtLjA1My0uNi0uMTA2LS45LS4xMDYtLjMgMC0uNi4wNTMtLjkuMTMzLS40MzYuMTA3LS44MTguMzItMS4xNDUuNTg3YS42MzIuNjMyIDAgMCAwLS4xNjQuMjkzTC4wMjcgNi41ODVjMCAuMDI2LS4wMjcuMDgtLjAyNy4xMzMgMCAuMjkzLjI0Ni41MzMuNTQ2LjUzM2EuNTU0LjU1NCAwIDAgMCAuNTE4LS40bC41NzItMi4zMnY3LjQ2N2gxLjA5MXYtNC44aC41NDZ2NC44aDEuMDlWNC41MDRsLjU3MyAyLjMyQS41NDEuNTQxIDAgMCAwIDYgNi42OTFjMC0uMDUzLS4wMjctLjEwNi0uMDI3LS4xMzN6IiBmaWxsPSJ0b21hdG8iIHN0cm9rZT0ic25vdyIgc3Ryb2tlLXdpZHRoPSIuMSIvPjwvc3ZnPg==' x='" & 16.5+100 * [新增] / MaxValue & "' height='12' width='6' />"
VAR SVG = "
    <svg xmlns='http://www.w3.org/2000/svg' viewbox='0 0 141 20' >" &
        Color & Chart & "
    </svg>"
RETURN
    SVG 
```

度量值中，rect生成条形，第一个text生成类别标签，第二个text生成数据标签，image生成人物图标，color变量产生渐变效果。将度量值放入HTML Content这个视觉对象，设计即完成。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6TcNWyxxEWcENibcZ7XTSLrxezGmAahR6fo6Vbo0ulgB0AVHqZH6b5xw0Hz5BSHtmxCcz7Q8u0YDsQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

动画演示：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/JHQQIBqYy6TcNWyxxEWcENibcZ7XTSLrxFwtBOiaSEIZwXOvO9twMoOlCRkwSFP5SibZFARPRhBoHBt1Me2OWfFbQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

本文PBIX源文件在下方知识星球下载。直达链接（左下角阅读原文也可访问）：_https://t.zsxq.com/09NG48LbQ_

