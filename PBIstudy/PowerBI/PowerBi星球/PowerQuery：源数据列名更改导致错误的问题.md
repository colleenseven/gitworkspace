---
ZK: Origin
notes: False
aliases: null
create_date: 2022-03-04T12:07:01 (UTC +08:00)
tags: wx/pbi/PQ数据处理
pagetitle: PowerQuery：源数据列名更改导致错误的问题
source: https://mp.weixin.qq.com/s/AVofvo20G6Atw_OgEaXIVQ
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

PowerQuery很强大，但也非常容易出错，尤其是初学者，经常会碰到不知道做了什么突然就报错了，然后就不知道怎么办，刚刚燃起的学习劲头可能因此而退却甚至放弃了，所以我将整理一些常见的错误以及解决的办法，帮你轻松应对各种报错问题。  

今天介绍一个很多人经常问的问题，<mark style="background: #FF5582A6;">源文件的列名修改以后，在PowerQuery中刷新很可能会报错</mark>，来看看这种情况该如何处理。

假设数据源是下面这个Excel文件，一个简易的订单表数据：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOPZbxrH46Myt8BibbywdWyjL8evyrZm5rPnZlJXtocAcuoz4bPUBPibyd0hdAJ0jc2QrU6hkX5C4Ug/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

导入到PQ以后是这样的界面：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOPZbxrH46Myt8BibbywdWyjvX9jTgoaldbn4YwAuxyrX7XKTwtymszCpicWlYRYLCjrrKMUD39dltA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

如果源数据格式不发生变动，刷新是正常的，不会出问题。

但是假如源数据的列名被修改了，比如最后一列的"金额"，修改成了"销售额"，PQ刷新后将报错：找不到表的"金额"列。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOPZbxrH46Myt8BibbywdWyjJfjT5tibMTh87TpwCPvqRB8UB02rabmK1GGyzibb05Hknhfc0ibibS3Cfw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

你肯定见到过这种错误，应该怎么处理呢？

最直接的方法就是将数据源修改的列名再改回来，如果无法修改源数据，你可以重新导入处理一遍，但是假如整理的步骤非常多，那么因为这个小小的错误而重新做一遍就太浪费时间了，其实我们只需要找出报错的步骤，相应的修改M公式就可以了。  

下面来看看如何修改M。  

从上到下用鼠标依次点击右侧的步骤，检查是从哪个步骤开始出错的，这里例子中，点到第三个步骤“更改的类型”，发现是在这个步骤开始报错的：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOPZbxrH46Myt8BibbywdWyjbZWT0qpISY0GB41rSIryL2qsReg21Xt3gobJkxl300cwYOlCKys2ZQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

然后在公式编辑栏中，可以看到有个代码是更改“金额”列的数据类型，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOPZbxrH46Myt8BibbywdWyjpfyfQNiaZmCby2ZO4ITs8fpE5gNVBdfYzrZMmlASqQmvicuklwX2WqNA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

但是由于数据中不存在这一列，所以导致报错了。

如果你提前并不清楚数据源的列名被更改过，那么也就不知道具体被更改成什么名字，这时可以去查看这个步骤的上一步，该列的列名到底是什么：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOPZbxrH46Myt8BibbywdWyjFtV3vBeFZBpzWfkicNbWibgol22wZ1wb2fdficCbW9QNibluH4qWcGLj2A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

点击上一步“提升的标题”，在这个界面，可以看到最后一列的列名是“销售额”，确实是不存在“金额”列，那么这个报错原因就很清楚了，只需要将“更改的类型”这个步骤公式中的“金额”，改成“销售额”就行了，报错消失：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOPZbxrH46Myt8BibbywdWyjDK4XzCtUlDadNAv3N6S7rSUX5o80yqadJ14DzwUibPE5fR3RXlAy2Ow/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这样就把错误解决了，并不需要去修改源文件或者重新导入一遍。  

其实熟练掌握以后，只需要根据这个报错信息，点几次鼠标就可以找到错误原因，不需一分钟就可以处理掉错误。

**以上方法不仅适用于修改列名引起的报错，只要你看到PQ界面出现报错，都可以按这种方式一个个步骤去排查，从出错步骤的编辑栏公式中找原因并相应修改。**

以上是直接将M中的原列名修改为新列名的方式，但是如果这个列名经常被改动，比如明天又被人改成了"金额"、后天又改成了"销售收入"，那么每次刷新都会报错，都要手动去修改也挺麻烦。  

还有一种做法是用M函数提取这一列的列名，比如这个示例中，最后一列的列名"销售额"，就是"提升的标题"这个步骤表的第4列，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOPZbxrH46Myt8BibbywdWyjL9YLux03Y1LzbgLLGktQiagesluEiaWSmXxdYS2EFm3wORzd3nlbHccg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

_"_提升的标题"这个步骤表的第4列的列名可以用这个M公式替代：  

**Table.ColumnNames(提升的标题){3}**

<mark style="background: #FF5582A6;">Table.ColumnNames返回表中所有列名组成的一个列表</mark>，PQ中，<mark style="background: #FF5582A6;">表是从0行开始的，第一行的行号是0，第4行的行号是3，所以上述公式中，提取列名表的第4行，用的是{3}。</mark>

然后将出错步骤的列名，也就是将之前错误的“金额”替换成这个M公式：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJOPZbxrH46Myt8BibbywdWyj4WEItwAQmKdhsiby4xUz1U02aBtjA9Q2JiczaluehWnTwiaoicbz8vuwibw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这样，无论源数据中第四列的列名被别人怎么改，都不会再报错了。

如果有其他列的列名同样可能会被修改，你都可以相应的将具体的列名替换为M公式，**只要在每个步骤的M中不出现源数据中具体的列名，PQ报错的概率就会大大降低。**  

不过这种方法的前提是你清楚哪列的列名可能会被更改、列的前后顺序位置是不变的，如果你的数据源每一列的列名都可能会被修改，甚至每一列的位置也会发生变动，那么这种方式就不适用了，可能还是需要你去检查出错的步骤手动修改。  

对于最后这种情况，我想你该做的不是去找各种PQ技巧去应对杂乱无规律的数据，而是去规范你的数据源，不要让别人随意更改，将格式固定下来才是明智的做法。
