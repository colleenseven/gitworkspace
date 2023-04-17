---
create_date: 2023-02-05T23:33:34 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases: null
pagetitle: Power BI模板文件，你用过吗？
source: https://mp.weixin.qq.com/s/ugGlhfQ0I7GjuaeS_nDYJg
author: 采悟
status: 已完成
category: 浏览文章
notes: False
ZK: Origin
uid: 
---

PowerBI文件的后缀是pbix，可能你还见过有一种文件的的后缀是pbit，这是什么文件呢？最近碰到有星友问到这个问题，这里就来介绍一下，其实带这种后缀的就是PowerBI模板文件。  

**PowerBI模板是什么？**

PowerBI模板文件后缀是pbit，包含了生成模板时该报告中的报表页面及其视觉对象、模型关系及其度量值以及PowerQuery查询步骤等，**简单来说，相对于生成它的pbix文件，pbit文件只是不含有数据，除此之外的元素都包含在模板文件中。**

**如何创建模板文件？**

有两种方式可以创建模板文件，打开需要创建模板的pbix文件，可以直接"另存为"，保存类型选择PowerBI模板文件（\*.pbit）:

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOrPdHRpAaq468cDe9PxdKHIJJEyZv2MG4vSWkoFErvVM4UyAUZe41icEojL9bMlW1A1qibxIvpz5bQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

或者选择导出>Power BI模板：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOrPdHRpAaq468cDe9PxdKHWKRiaIugMcNCJG6MicibFpjdMeMXXYJFiapa75muJgf7YNlicgHsIYOjTMQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后在弹出的窗口中，可以对这个模板填写必要的说明信息，点击确定就生成了该文件的模板文件。

**如何使用PowerBI模板？**

直接双击打开pbit文件，或者通过导入“PowerBI模板”的方式打开：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOrPdHRpAaq468cDe9PxdKHuXy3F8X2piceore9QnAO72UMzoF3D5ETyeaeGN104w3VIX5xOiazGibGw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果原创建模板的报告没有PowerQuery参数，也无法连上数据源，则会打开一个无数据的空白报告，只能看到报表页和模型关系。进入PowerQuery编辑器中连接上数据源以后，报告才会正确显示出来。  

如果==原创建模板的报告有PowerQuery参数，则打开模板文件后会自动弹出一个窗口，要求输入参数==，比如将源数据的路径设置为参数，打开pbit文件后，会自动弹出这样的窗口：  
![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOrPdHRpAaq468cDe9PxdKHYObibf3wRPrJeuknhkPSsX6a7iaWeefVkibDJDj2fN68EQQtCicGmFAkfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOrPdHRpAaq468cDe9PxdKHYObibf3wRPrJeuknhkPSsX6a7iaWeefVkibDJDj2fN68EQQtCicGmFAkfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)
正确输入路径，点击“加载”，然后报告就会完整呈现出来。  

**PowerBI模板的作用？**

如果很多部门有相同的数据结构，则可以通过制作好的模板文件分享给他们，每个部门收到模板文件后，只需要导入自己的数据就可以自动生成各自部门的报告，他们还可以在此基础上继续开发、完善报告内容。

并且无数据的模板文件，相比带数据集的动辄几百M甚至几个G的pbix文件，更加轻巧，分享起来更加便捷。

关于pbit模板文件还有个好用的场景是，==制作PowerBI报告时，设置路径参数，再生成模板文件；分享时不是直接发pbix文件，而是发pbit文件和数据源，然后对方打开模板时，自动弹出提示窗口，要求输入数据源的路径，而不需要进入PowerQuery编辑器，更加直观便捷，对不是很了解PowerBI操作的用户也更加友好。  ==
