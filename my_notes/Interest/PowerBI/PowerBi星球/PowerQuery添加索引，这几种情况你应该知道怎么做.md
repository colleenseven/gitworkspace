---
ZK: Origin
notes: False
aliases: null
create_date: 2022-04-06T11:55:57 (UTC +08:00)
tags: wx/pbi/PQ数据处理
pagetitle: PowerQuery添加索引，这几种情况你应该知道怎么做
source: https://mp.weixin.qq.com/s/GLsuZ4SZ3np_Xq4Bj6cvEA
author: 采悟
status: 已完成
category: 泛读文章
uid: 
---


为了更方面的进行数据分析，经常会有<mark style="background: #FF5582A6;">为表格添加索引编号的需求</mark>，利用Power Query添加索引十分简单，因为界面上直接就有添加索引列的功能。

比如下面的数据，点击添加列>索引列，轻松就可以添加一个连续编号的列：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMwePy6LrpicIoFGbAoAQRmdxDP2D3tpo5GPIKkrxPviaAtDcNiaPAkDaRDBujjDp94Kuu1wlSojkia3A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面是对表的每一行按顺序添加索引，但是实际情况或许并不总是这么简单，我就经常被问到如何<mark style="background: #FF5582A6;">按类别添加索引的问题</mark>，比如下面两种情况。

如果数据变成下面这样的，  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9ka8opo91al7Np9cIwP7HO8Hguv7aKmsq3b9vuITALty6vBfj5140vj5Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

需要按类别添加1、2、3、1、2、3……这样循坏的索引，应该怎么做呢？

同样可以先正常添加一列索引：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9kaTcs1gl0ZWw3vn9bFXuw7WibY6kSwN5Dz8QB4IIeGHw3cTCJe8ibxiaL4g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后再添加一个<mark style="background: #FF5582A6;">自定义列</mark>：

\=Number.Mod(\[索引\]+2, 3)+1

也就是<mark style="background: #FF5582A6;">计算索引除以3的余数，即可得到每三行一循环的索引编号</mark>，不过正常除以3的余数是1、2、0，通过Number.Mod(\[索引\]+2, 3)+1就可以变成1、2、3：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9kaWoVvCoibcvJPibDibiaqj6SWOPOMWAcE8OHjhv6VWP3kmsRmfsia2qoIicHw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

上面的情况，表格的数据还是有一定规律的，每三行一个类别，如果完全没有规律，每个类别的行数不一致，如下图：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9ka0UwHmkTOYWQeEeSDXbVf9KclJpNBPXDp1rfOCdA0Zv8NRAia6IMJarw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于这样的数据如何按类别来添加索引呢？

只需要以下两个步骤：  

**1\. <mark style="background: #FF5582A6;">分组</mark>**

点击转换>分组依据，按类别分组：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9kaejkSR61MneUYr4odMdoqKGz9FxiaZzNP1wpeAPNYrdiazGJm5qeZp9cg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

其中操作要选择“<mark style="background: #FF5582A6;">所有行</mark>”。  

**2\. 修改M公式**

对于上面的分组，你会在编辑栏看到M公式：

\= Table.Group(源, {"类别"}, {{"计数", each \_, type table \[类别=nullable text\]}})

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9kaXoBvK9UUicHQWmBNDrwE3l8HzVFKOGlIMDUmoibwz1Pu7UecwhrD1uzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

只需将这个公式修改一下:

-   将下划线 **\_** ，替换为**Table.AddIndexColumn( \_,"索引",1,1 )**
    
-   将 \[类别=nullable text\] 删掉
    

也就是变成下图编辑栏中的公式：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9kaRVqCBJPDqQcGcgoeoAfRa6Z52VyU1aHMAfVdx0JB6aKMMWM1ERRh2g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这里用的<mark style="background: #FF5582A6;">Table.AddIndexColumn其实与正常添加索引用到的函数一样，只是这里的用法，是在**分组后未展开的Table中，添加一列索引**</mark>。

点击每一行的Table，你就能看到带有索引的表：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9kaHMia3ZO01skFwXiauy5HbXPASfzcKv3MMS6cjHY8A8AraoEHQFgVqsRw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击计数列右侧的展开按钮：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9kaZ6rNNa8nonUk2qESzVib6wJSnet5AlegGPCAXzsvMYvpoUtaujVna4g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

只勾选“索引”列即可得到最终的结果：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPTQASDJdiaZC0tOibTb9b9kadibHYGP3iagI09NkW9rRdAqxQJaCgicel0sFxHW7ppHCr5pOgZjZGC6ew/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

对于按类别添加编号，最下面的这种方式才更普适，如果你有类似的需求，不妨试一下。
