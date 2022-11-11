---
aliases: null
create_date: 2022-02-24T12:22:20 (UTC +08:00)
tags: 
pagetitle: 利用Power Automate，轻松下载PowerBI报告中的数据
source: https://mp.weixin.qq.com/s/lHYDxzRExLproMfcnHKVRw
author: 采悟
status: 未阅读
category: 
uid: 
---

Power Automate是微软的流程自动化(RPA)工具，可以友好、无代码的实现各种低效工作流程的自动化处理。它也已经集成到了PowerBI中，在 Power BI 报表中创建 Power Automate 视觉对象后，终端用户只需单击报表中的按钮即可运行自动化流。

通过二者的协同，可以提供更强大、更灵活的解决方案，我会通过一些实用的应用场景来介绍他们的用法，今天分享一个利用Power Automate导出PowerBI报告数据的案例。

PowerBI的可视化图表中的数据可以导出来，不过这个功能并不直观，应用场景有限，如果**在报告页面上添加一个按钮，让终端用户点击即可下载数据**，是不是就方便多了？

___

首先说明一下，这里介绍的导出数据，并不是将数据导出到本地，而是导出到onedrive上，你首先需要拥有onedrive for business账户。

___

本文以之前介绍过的这个[客户细分](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071357&idx=1&sn=e533d335e302b9ca5c76313dcac38852&chksm=8e0c416ab97bc87c1101fcbdb870356d9a400c68ba7c8ab6b91d4e6c54726b28cc358b6015fd&scene=21#wechat_redirect)报表为例，来演示一下如何为页面上添加一个“导出数据”的功能按钮，如下图：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtG0abKWCwdKUUUpv0j8yCLHRYgZafMqJGmTkEJnajU3RznDkmcxficIw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

右上角的“导出数据”按钮

下面来看看具体实现步骤：

**一、在报表中添加 Power Automate 视觉对象**

点击可视化面板中的Power Automate，将它添加到画布上，  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLteScQSd0wRu1zxchvLLk4Vph5licjZctPm3YS5vmocDpL6ftGFcY0pPg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后会出现一个窗口，说明它的用法和步骤，首先添加数据，将需要导出的数据字段都拖拽到字段框中：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtdjreGnjiaTZfrGzvrQtoIUrgziavnMQtQIetukuNmicC1xKca7uxsRu6A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**二、编辑流**

点击该对象右上角的三个点（...）,选择“编辑”，  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtuibm9pKxASGu1TVl6yPiaZH2kHSGEvwOKT1aYDCdX3bBNoM3sqes7D5g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

进入编辑窗口：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtbpgQ03wiczYyicgqjEJyiaO83bjY6h9TUg1Ipw39lG8c4MJr86mETmMGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

可以点击左上角的“新建”、也可以利用下方的几个模板来创建工作流，这里我选择利用模板，下面开始真正开始编辑工作流：

**1\. 点击左下角的模板：从PowerBI更新Excel表**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtputJZ8ib2SKt0xML65nwbmYk6MedEbWjUTEX3vbvQFhicLrcXMgrHAjg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

Excel Online可以理解为onedrive上的Excel，在这个界面，参考上图的箭头，点击Excel Online右侧的三个点，登录自己的onedrive for business账户，然后点击“Continue”。

**2\. 删除现有的步骤**

删除步骤“Update a row”：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtv5R7vFfSsoBDCbvak6PEA6AD7N2Sibzzzo3pmPZM8teTDJpqw44zibbA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**3\. 添加步骤①：编辑**

点击New step，搜索并找到“编辑”：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtju5fKKZoOFickPCsiavtbVAspt2smhkb82oDufLk33pStzLcWVTVUzfg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击“输入”栏，在弹出的窗口中，选择最后一项“PowerBI 表”：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLt1icGncib8dFsmpIJiaQv8JZ8aZMUGcNaa9AvT8zv0sa6V6IMywz39SnzA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

### **4\. 添加步骤②：创建csv表格**

搜索并找到“创建csv表格”的操作：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtrhn59VQqnKWbwOVS3pcXiaHK15icnJjuTVFgXU1RcR9wgSMumb4QJrxw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

在“From”栏，在弹出的窗口中选择上一步的“Outputs”：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtJLm6iavCbgPKYKicoytk9dmf3fsxILGstxp78pq64fqRNrRibVVjVQDoQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**5\. 添加步骤③：创建文件**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtEo6sQt1b2icY1YVga9eBNeJtgMw2A8GAX0s9BzCianF3DuTK7H2ZSUrQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

在编辑界面中，分别填入下面三项：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtoicEUgDL0WKhuxXdwEI61XVrmZz9AY4LDrATAbssHicq9HPoEiapsRZYA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

-   **文件夹路径**：点击右侧的文件夹图标，可以选择onedrive中已有的文件夹；  
    
-   **文件名**：可以任意命名，如果是个静态的名称，则每次导出后会自动覆盖上次导出的数据，这里我选择了把时间戳(可以在弹出的窗口中选择)作为名称的一部分，这样每次导出都是一个新的文件名，不会覆盖原有的。另外，后缀.csv不能省略；  
    
-   **文件内容**：选择上个步骤的输出结果Output。
    

然后点击“保存并应用”，至此整个工作流编辑完成。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOuicKy2vCw9gcReA6z1ibdstQHP46hV0iaSP5EEyicHyS0HRSUw8GfFNgibmgTaXiaib2ibyRMuIMDbJoianA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**三、设置按钮格式**

上面的步骤完成并返回到报表页面以后，就会看到页面上已经出现了一个大大的蓝色按钮，可以调整按钮的大小，并选中按钮，在格式面板中调整按钮的文本以及填充颜色：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtNMJDrn7Lcc7VNCpPKj8wjQaJnFylnXOSFolhMpWc8GRos3WuNK8eYA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这里我把按钮的文本改成了“导出数据”：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtftwVdP7FSyTDFr41eBoGWyAr5BKH7gFBXRo8tBCBWicoHqs7aTzxADw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这个Power Automate按钮与正常添加的按钮用法是一样的，在PowerBI Desktop中需要按住Ctrl点击，发布后直接点击即可触发。  

点击后就可以在onedrive相应的文件夹中看到下载的数据：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJO2EGr1hzqzwPPpicP9A8kLtNa6PVI261ibdfLiaHjMAQA6qGxJ0QRutVxYgFFiaYZkVSLwib3wkRECQZA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这里有4个文件，就是我在不同的时间分别点击了四次，生成了不同名的csv文件，并且这里**导出的数据是动态的，是基于最终用户点击各种筛选器交互后的数据。**  

___

**说明**：这里导出的是csv文件，里面的中文直接打开可能会乱码，可以先下载到本地，然后用excel导入csv/文本的方式打开，具体操作方法可以搜索一下。

___

以上就是利用Power Automate下载PowerBI数据的技巧，全程鼠标点击，无需任何代码，轻松在PowerBI报告中添加了一个下载按钮；如果你制作完成点击按钮后，没有在onedrive中看到下载的数据，或许是上面某个步骤操作有误，请再仔细看一遍操作步骤吧。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
