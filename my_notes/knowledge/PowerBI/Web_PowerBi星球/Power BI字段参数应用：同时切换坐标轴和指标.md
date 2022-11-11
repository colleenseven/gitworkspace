---
aliases: null
create_date: 2022-06-01T12:34:04 (UTC +08:00)
tags: 
pagetitle: Power BI字段参数应用：同时切换坐标轴和指标
source: https://mp.weixin.qq.com/s/PQPH_-rCF3uCWzpXsG8tWQ
author: 采悟
status: 未阅读
category: 
uid: 
---

上周介绍了新推出的[字段参数的基本用法](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080273&idx=1&sn=b985ea8a53854f41a1ba75c0585cb3cd&chksm=8e13a446b9642d5085b1590f38ca7dd36c085269ae2d5d0fe75e09c57fc1ae270158d15d79db&scene=21#wechat_redirect)，利用它可以方便的进行动态的分析，比如动态坐标轴、动态指标等，然后有星友问，能不能在一个图表中同时切换坐标轴和指标呢？  

这种需求看起来也并不难，只需要把把坐标轴和值里面的字段，都用字段参数即可，比如已经建了两个参数，一个参数是产品名称和城市两个维度字段，命名为坐标轴：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMP6F6LPwbTGIZ5zF214qoFhGOuqY7efbqYBNRIpmZbYkUvoz4HTVKt5jbfjibA9GkZEibwLeqpUbGg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

另一个参数是销售额和利润两个度量值，命名为指标：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMP6F6LPwbTGIZ5zF214qoF1Yaz5ibJuMaB6LtgzKfN5Z2WDHB8WVAFibzK1aPhSiccOFHMEgdTTic6qQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

分别将两个参数放到柱形图的X轴和Y轴上：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMP6F6LPwbTGIZ5zF214qoFhlWEt3E1NdTQBkpHicFUPKLVvN4bVo6O6icPDRrbXxOzVQibvHFEFX8Jg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后通过点击坐标轴切片器器和指标切片器，就能在一个图表上实现坐标轴和指标的动态切换。  

**不过这个需求的关键是：同时**。通过两个切片器并没有做到**同时**切换坐标轴和指标，而是先切换一个，然后再切换另一个。

**想做到同时切换，必须只使用一个切片器，既能控制坐标轴，又能同时控制指标。**

一次同时控制坐标轴和指标，而坐标轴和指标分别有两个类别，共计有四种组合，就需要一个字段上同时有这些选项：

-   产品销售额
    
-   产品利润  
    
-   城市销售额
    
-   城市利润
    

那么就可以修改字段参数，将每一种组合都列出来，首先修改坐标轴参数，直接修改生成参数的DAX公式：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMP6F6LPwbTGIZ5zF214qoFgCL2kf64b7qjFtQZRb1VazIKvjmnq3EP3ME3yTchicLfPulvc0YGW2w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**就是将原来的两行参数再复制出来两行，变成四行，然后添加一列，将二者的组合手动写进去，并重命名该列为\[场景\]。**  

同样的方式，修改指标参数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMP6F6LPwbTGIZ5zF214qoFveEeWds3AR63ic24QhuHKcfQmIWlNTcrSWqBgf7vsQC5CCCWpDibqFqA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**注意两个表的场景要对应上，比如城市销售额这个场景，在坐标轴参数中对应的是城市、在指标参数中对应的是销售额。**  

然后会在页面上出现两个切片器，这时可以利用[同步切片器](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068670&idx=1&sn=c3058974e1651626ff2a80a318e6e7da&chksm=8e0c4be9b97bc2ff1cccdb26a04e84534eb3c129776ef26e71c99459ab57e54c006debfb3b2c&scene=21#wechat_redirect)将它们变成一个分组，先选中第一个切片器，打开同步切片器面板，展开高级选项，输入同步切片器组名，这里命名为“场景切片器组”：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMP6F6LPwbTGIZ5zF214qoF3N9KcKKicUic3FVm0o9rPgSJpJsCaibIicQlCwvhzZLKvGnjsJsq5b6how/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后选中第二个切片器，命名为同样的组名。

这样设置完成以后，两个切片器就能同步联动：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMP6F6LPwbTGIZ5zF214qoFIFYyEgtkyu1Y8SYhSN4icIFvtrbHDljlVuxBwznaib6sia0ib3IDLI5tjg/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

因为两个切片器是同步变化的，所以只需要一个切片器，将另一个切片器隐藏起来就可以了，这样就实现了坐标轴和指标的同步变动。  

___

其实还有个更简单的方法，不需要设置切片器同步，只需要在两个参数表之间，利用场景字段建立关系，  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMP6F6LPwbTGIZ5zF214qoFibklxrq1PmhniaRPcibNpU1tAfkW4yDybOzW2YdBicZ1xMj8GeULREtG3g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

同样也可以实现一个切片器同时切换坐标轴和指标的效果：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMP6F6LPwbTGIZ5zF214qoFa9duj7M65p03bgJvFrBCNLQ3jJJk2tug0qbVZhVm40kqlVm9GAPjEg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上就是字段参数的另一个应用场景，掌握它的用法，有助于你进一步理解字段参数。

___

[**PowerBI商业数据分析**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)

帮你从0到1，轻松上手PowerBI

___

**如果你对PowerBI感兴趣，欢迎加入我的PowerBI学习社群****，获取更多学习资源，和4500+ 爱好者一起精进~**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJO1AEySOiakLF2kY7eb1kUw2DtfKoVz2ctBDia5dtNsPX2GhV0ZOCDDWpgpaTQtnqfqJrRXt5PNia95g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如你刚开始接触Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门Power BI》电子书，轻松入门。
