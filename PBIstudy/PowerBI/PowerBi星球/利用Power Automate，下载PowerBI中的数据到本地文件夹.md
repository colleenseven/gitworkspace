---
ZK: Origin
notes: False
aliases: null
create_date: 2022-06-30T12:29:41 (UTC +08:00)
tags: wx/pbi/数据处理功能
pagetitle: 利用Power Automate，下载PowerBI中的数据到本地文件夹
source: https://mp.weixin.qq.com/s/WXADkDL8rYPqf2NL0i7PFw
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

之前介绍过利用Power Automate，在PowerBI报表中添加了一个下载按钮，动态下载报表中的数据：[利用Power Automate，轻松下载PowerBI报告中的数据](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079238&idx=1&sn=0ae06ab03c215c59ad020c81e7983aa5&chksm=8e13a051b9642947c66a83ec8efdd230b2215d019a6d69100e4eed21f16b03e1fe03d3e862a7&scene=21#wechat_redirect)。

不过它是将下载的数据放到了OneDrive中，得先拥有Onedrive账户才能使用这个方法。很多人恰恰是没有合适的Onedrive账户，所以经常有人问，能不能直接下载到本地文件夹呢？本文就介绍一个将PowerBI数据下载到本地文件夹的方法。

本文介绍的方法虽然不需要使用OneDrive，但也不是完全无条件自由下载，它需要使用数据网关。

<mark style="background: #FF5582A6;">数据网关是本地数据和云端数据连接的纽带</mark>，**之前我们介绍过<mark style="background: #FF5582A6;">利用数据网关将本地数据传送到云端，以实现云端的计划刷新；而这里的使用场景正好相反，是将云端的数据传输到本地</mark>。**

关于数据网关的介绍，参考这篇文章：

[利用网关实现Power BI报告的自动刷新](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484076890&idx=1&sn=d50a0875dccb56423464b2af3742bd36&chksm=8e13ab8db964229bfc354e4039f72370bfe6cde7b43fd87dc11062a8bcd72cf35e7f2cc44cc4&scene=21#wechat_redirect)

网关安装好并登录账户以后，会看到这个界面，表示网关环境准备就绪。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNXPy1lnBdpT8B0VdNS9tV4oG0nN9cjaMrIic0OCiaNABT6SOtGbuf1LYickgm4icMq7IbjvNBIapibOmg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后就可以开始进行下面的操作了。

还是用[前面文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079238&idx=1&sn=0ae06ab03c215c59ad020c81e7983aa5&chksm=8e13a051b9642947c66a83ec8efdd230b2215d019a6d69100e4eed21f16b03e1fe03d3e862a7&scene=21#wechat_redirect)的示例，只是更改下载文件的目标位置，除了下面这一个步骤，其他步骤和之间的介绍完全一致，如果你还不熟悉，可以先看这篇文章：

[**利用Power Automate，轻松下载PowerBI报告中的数据**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079238&idx=1&sn=0ae06ab03c215c59ad020c81e7983aa5&chksm=8e13a051b9642947c66a83ec8efdd230b2215d019a6d69100e4eed21f16b03e1fe03d3e862a7&scene=21#wechat_redirect)  

下载到本地只需要修改这一个步骤。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNXPy1lnBdpT8B0VdNS9tV4s7C9yBu9cmvNGEYezNm9TsU8XjfLTBibS7hKSSE7jqumywDwu5VtLUg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个步骤是在目标存储中创建文件，之前用OneDrive的时候，点击的是上图中的在OneDrive for Business中创建文件这个操作，本文是需要在本地创建文件，所以更换这个操作即可，下面是具体步骤。  

___

**5\. 添加步骤③：创建文件****（本地文件夹）**

选择"File System"的创建文件，如下图。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNXPy1lnBdpT8B0VdNS9tV4TVsAdtIvxo46gs0dY9F1ffJAVrdE0lbMrf2iaFWKc78yuJTSOjicuiaGA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

在弹出的窗口中，配置本地电脑和文件夹信息，具体填写细节如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNXPy1lnBdpT8B0VdNS9tV4V9icCw9dSRnkh6BicZZbLfPMDNjZrL4ibQRYd1DhqRQXvZxzDQeCYWP5A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

点击“Create”创建连接，接着在窗口中输入下载文件的信息：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNXPy1lnBdpT8B0VdNS9tV4UK4HgUeg2hyiaHHohIvRic7iay5EkJIZDoj6HQegf1I0yeVDXjRRJvlHQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于文件名，如果是固定的，则每次下载都会覆盖掉之前的下载文件，如果想保留之前的，可以在文件名中添加个日期参数，表达式如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNXPy1lnBdpT8B0VdNS9tV4tEpE4Dm3D6PYtebEZG22qAY1CMn8zSlU21mZ2Pkt2hVXoQPwQa3t2Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后文件名中就会有个动态的日期：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNXPy1lnBdpT8B0VdNS9tV47P4MEk95vaOwvmVaFkv1MevA4KvHFfWbxazGW2hsjCttySK7HRHZAw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样每天下载的文件都会带上当天日期，不会覆盖掉之前日期下载的文件。

至此，本步骤修改完成，剩下的步骤，与[之前文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079238&idx=1&sn=0ae06ab03c215c59ad020c81e7983aa5&chksm=8e13a051b9642947c66a83ec8efdd230b2215d019a6d69100e4eed21f16b03e1fe03d3e862a7&scene=21#wechat_redirect)完全一致。  

___

然后当你在页面上点击“导出数据”的按钮时：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNXPy1lnBdpT8B0VdNS9tV47R4RwyTjTcYiaFp5Fp31vL9PJfrymNZjKQCILQzeX6OTOh6UDtBCoyg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

将自动在本地目标文件夹中创建一个csv文件，其中的数据同样是动态的。

___

关于csv文件，直接用Excel打开，中文可能会乱码，如果你遇到这种情况，不要用Excel直接打开，而是打开一个空白的Excel文件，进入【数据】选项卡，点击“从文本/CSV”获取数据，然后选择对应csv文件即可。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNXPy1lnBdpT8B0VdNS9tV4ZrmTPAVkfbZkiaBp09Vme3yJwvybFAKicZiceYf4xXcy3ofrRA0EyVZJA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上就是将PowerBI中的数据下载到本地文件夹中的方法，配置好数据网关以后，只是一些简单的操作步骤，如果你有这种需求，可以动手尝试一下。  

___

