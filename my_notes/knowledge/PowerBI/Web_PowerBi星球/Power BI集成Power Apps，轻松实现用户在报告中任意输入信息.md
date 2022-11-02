---
create_date: 2022-03-15T11:58:58 (UTC +08:00)
tags: 
pagetitle: Power BI集成Power Apps，轻松实现用户在报告中任意输入信息
source: https://mp.weixin.qq.com/s/9LO_8V_mU4nnKeql98MIWw
author: 采悟
status: 未阅读
category: 
uid: 
---

PowerBI报告很强大，但通常情况下它的信息是单向传递的，由报告制作者通过报表上的数据向用户传递信息，用户可以在报告上交互图表，但并不能在报告上添加信息，这也是很多人期待的一个功能。  

虽然PowerBI本身不支持让用户输入数据，不过利用Power家族的另外一个应用：**Power Apps**，也是可以轻松实现这个需求的。

以下面这个报告为例，展示了每个产品的环比增长数据：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qYtQ4pbg6RTr4AF6Xw6zZDErhenFXmCjicDU0wHzv3HgHEzEhSLQ7hlw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

假如把这个报告发给领导，领导看到后，可能想会对部分产品提出处理建议，怎么在PowerBI中添加个输入框让领导输入文字呢？

下面将利用Power Apps来实现这个需求，这个方法的前提条件是，需要有Onedrive for business账户，并拥有Power Apps许可证。

**其基本原理是用户输入的信息，通过Power Apps将数据回写到onedrive上，然后PowerBI连接Onedrive上的数据，并呈现在可视化报告上。**  

___

**一、准备工作**

首先在Onedrive for business上建一个表格，这里我命名为“备注表”，有产品名称和备注两列，为了让Power Apps识别到它，需要将这个数据转换为智能表，套用样式就可以了：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qRn2H5SIl2NYFicVK2LCz5y2DrXOGVOCXFSic2JV9ZFEfvRlw9iaxY288A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这里的备注列什么数据都没有，就是为了下面进行回写而准备的。

然后利用PowerBI连接onedrive上的这个表格，连接方法参考：[Power BI如何连接OneDrive？这个极简教程分享给你](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078309&idx=1&sn=acead16f62436ec048acb62295b134c6&chksm=8e13ac32b96425240657c76d62d40ffdc635a94b9de007b9f5d8d31ca0cd60e27fdcf1f99d76&scene=21#wechat_redirect)  

导入到模型以后，将这个表与原模型中的产品表建立关系：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qibG6BjUzWhP86iaY09k305AeW3OCzicTWpJLuQsAgGicYA434QLc5sYLDw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后就可以把备注表中的“备注”列，放到前面表格里：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qvafpLAGC7EcUbWr75ic7VsHD54QnpHU2wsyZiaQtYKic2EBeYpHibsWrKg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

现在还没有添加备注信息，所以这一列都是空的。

___

**二、利用Power Apps创建应用**

画布上添加Power Apps视觉对象：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6q39qFKk33R0JkHFxOlSVsHSyAdsB3kgcwBv33QgCKmo6ej1ToUCa5kA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

将产品表中的字段“产品名称”放进来，待系统配置好环境以后，点击“新建”，  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qp2h1KGdt4DTZ5x0DytoIuPo0Y7dU7qMgk6RaQj2tS4EFRmowBN1fqA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

稍后会弹出一长串网址，点击确定进入Power Apps云端，进去之后，将现有的图层“Gallery1”删除：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qVY2Nht3ZakiaSD6TiaukXmgm33sWwoZy5gXR5majiahYwa1BdiaS3gicDCw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后就是一个空白的画布，我们重新开始建应用。

**1\. 插入>窗体>编辑**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qzVHx6Piceicaqrfkajs6uYzxTiaiclBHLFrntbSEUMtU2G9jk8icN0iaXlDg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. 连接数据源**

点击新建的编辑框，然后在属性>数据源>连接符，选择onedrive for business  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qyB2R3nicbaulwCJXaqOV54yrMKQSnT2hMuKAlksupqMGIicv9Ox9ALhg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后选择onedrive里面提前建好的“备注表”。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qfqVSXiayDHd8Ra3Qpj2jChBq6SNfUicibzKIdejTiaKQY1cuwSJNvwVuXg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**3\. 添加字段。**

将备注表中的两个字段都添加进来。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6q4YRgBZagLh4l45z2libKestB5U3jkBLQRk8csyKyzsIb5wPBx1MEePw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后画布上就出现有两个字段框。

**4\. 利用公式获取PowerBI上下文**

为了让上面建立的窗体获取PowerBI的上下文，还需要写个公式，点击左侧的图层Form1，在上面的下拉框中选择Item，然后输入公式：

> LookUp(备注表,产品名称=First(PowerBIIntegration.Data).产品名称)

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qaBG6iaLKFETKkfUNgR540DKIyE0QLCaelywJrbYCplUKMmtydYC1e9A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

它的逻辑是通过PowerBI上下文中的产品名称来查找备注表的信息。  

**5\. 添加按钮**

信息输入以后，还需要有一个按钮动作来提交信息，所以需要在画布上插入一个按钮：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qAGoTyDCjByFc8Ihn83ufsgSibgtD87qpKu4FmNgLlnW4ejOT1TIgsJg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于按钮的文本和格式，可以在右侧格式面板中设置：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qmOLAZTRrwcjiaGN1Dw1GntCDVwNuum67FAxRl9FgQah6r1CDEmrIicPA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后设置按钮的操作属性，上面的公式栏输入：

> SubmitForm(Form1)

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6q3qRB27zTuJVNFCibMGcfebvEZqHLibnGFQNb3icSjiawbQnoSO48n7icSaQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**6\. 应用设计**

可以在画布上方插入一个标题，看起来更美观，直接点击上方的插入>标签。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qEh4ukSH7d1tQjWv1M0EBic5YDy7CmEasXyDs4MLp9lTc9KiccsBpxZGw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

另外，这里还插入了一个文本框，以便提示用户正确操作。  

**7\. 保存并发布**

点击"文件"，选择另存为到云端：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6q7ibqLiczeadTQ5TxSVeKc12DFRgmkoY6XE2YNsNjZ1E2iamTwVgerzKhw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后在右下角点击保存即可。  

至此该应用创建完成。

返回到PowerBI报表页，就可以看到这个应用。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6q8h1Y0icrE7jPfLZtfWBPJDEXuKJWbgK18R7bX8q2jcOwrCsNmkaSehQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

___

**三、测试应用效果**

先选择一个产品，再对该产品做备注，比如选择环比降幅最大的“VR眼镜”，在备注中输入：

_请市场部解释原因并拿出扭转方案！_

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qUzZA4bKIdcib3PyqvcmG5Yt1XQMmxibGZjF1XibBDJYmD3mPlmUaHesqw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击“确认”，这个备注信息将回写到Onedrive中。  

这时表格里并不会立即出现这个文字，因为报表没有刷新，先刷新报表，或者只刷新“备注表”，  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qt9nl5vflQ3A289sfSL0fwS5x25micb7XUjJTKCt0q7DlBiavsy3wosuQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后Onedrive中的数据导入进来，表格的备注栏就会出现刚才输入的文字：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOQktx5oVg5n72ovsTjJD6qsbZO760K4GiasBc9YNoQ3W5RUXLf2aUhnh9ZIhKEt2voQ8NQkWiayibrw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

将这个报告发出后，用户就可以在PowerBI页面上面直接输入意见，其他人只要刷新报表，就可以看到对方的意见，是不是非常实用呢？

以上就是PowerBI集成Power Apps的一个经典应用场景，这里主要介绍了如何创建应用，具体细节你还可以继续优化，如果采用直连模式可设置自动刷新、利用书签来弹出/隐藏Power Apps应用窗口等，本文篇幅有限，就不再详细介绍。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4000+ 爱好者一起精进~**  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFLnwgdbghRHPLicKRaV70mVCZVq8Fhm46rkciaeOrLFJCv5f1omJxF8256YogHflkicEDM29aUMtaA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。
