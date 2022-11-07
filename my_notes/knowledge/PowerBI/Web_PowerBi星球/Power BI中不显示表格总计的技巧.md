---
create_date: 2022-10-16T23:14:50 (UTC +08:00)
tags: wx/pbi/建模技巧
pagetitle: Power BI中不显示表格总计的技巧
source: https://mp.weixin.qq.com/s/phP28WetvTpZGH2O3sSzSA
author: 采悟
status: 已完成 
category: 精读文章
uid: 
---

在PowerBI中经常会用到表格，如果里面有<mark style="background: #FFB86CA6;">数值型的字段，默认会显示总计行</mark>，比如下面这个表格，展示每个产品类别的收入和利润：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOna3LZzcEpp19wiaIJrARcpMngxGqw8yyHyic6PJfVgho5Q4fkf6WjsOkOE7sFZQZ24TTKUOeia7LlA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

其中产品类别是列字段，收入和利润是两个度量值。

如果打算去掉总计行，这个比较简单，只需要进入格式窗格，展开“总计”的设置，将值直接关掉就可以了：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOna3LZzcEpp19wiaIJrARcpTr4QacDsCAGSNQicpR2jWJah3aibOZObks2Uv95mfg0dFLUvYZ2tHyTQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**但是如果并不打算全部取消总计行，只想让某一列不显示总计，应该怎么做呢？**

比如上表，需要显示总计行，但不需要显示收入这一列的总计，下面用两种方式来实现。  

### **1\. 利用DAX让总计行返回空值**

对于收入度量值，<mark style="background: #FF5582A6;">可以通过ISINSCOPE函数来判断上下文是否为总计行，如果是总计行，则返回空值。
</mark>
度量值的写法以及效果如下。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOna3LZzcEpp19wiaIJrARcpIhVrnkibZKVwqeLGZh4cH64cAzTKSBffmvf5d2NTRcdTkfEOgs1Wygg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于利用DAX来处理总计行的更多场景，可以参考：[一文掌握Power BI矩阵总计的自定义计算](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078406&idx=1&sn=3f64d35e34d0f9cd0d5483ee46bf124a&chksm=8e13ad91b9642487e4c2e64af7c944c76ef506eab1a9ecb731173a3cbfbf57b46da9c2cd855e&scene=21#wechat_redirect) 

### **2. 利用条件格式隐藏总计行**

如果不想显示某一列的总计，还可以通过下面的设置来实现。  

展开“单元格元素”，选择不需要显示总计的列（这里是收入），打开字体颜色：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOna3LZzcEpp19wiaIJrARcpFO8mTueKWl6LLOwjJVyPW3os9ib9vSRIYhZ01bUm3tlq1JRym5RtL6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击字体颜色的"**fx**"按钮，进入字体颜色设置编辑框，在里面进行如下的设置：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOna3LZzcEpp19wiaIJrARcp2Ria0wMjfrEa6tM6cUibdtrcZfTUJodibvXbiclUN3sSIgFjHRaVZd1SBw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

也就是将颜色设置仅应用于总计，并将最大值和最小值都设置为与背景色一致的颜色（这里背景是白色，所以字体颜色也设置为白色），就可以与第1种方法一样，实现收入总计不显示的效果。

这种方式其实并没有隐藏收入的总计，只是总计的颜色与背景色一致，所以看不到了而已，该方式的好处是不需要写DAX，只需点击几下鼠标就可以实现，非常方便。

上面两个技巧，你学会了吗？

关于表格/矩阵的更多设置技巧，请参考：  

[Power BI矩阵格式设置13招](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071983&idx=1&sn=3fd379f7bf88141747ac9a09dc4273b7&chksm=8e0c44f8b97bcdee4cb068fd1e47e033629cf0734dd29c8341746d449372068dbb4e6d298cba&scene=21#wechat_redirect)  

[一文掌握Power BI矩阵的自定义配色](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078467&idx=1&sn=ad4e9834b50b19df4b0d79d156dfe0b3&chksm=8e13ad54b964244279a717fb8ddaa704cc3b5a1bf6f63fb377dd1f2d7c97f4c868b14d7799c5&scene=21#wechat_redirect)  

[PowerBI矩阵可视化技巧：总计显示在左侧+动态显示列](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484079444&idx=1&sn=ad080b098e66a4ce4e2c6183cc4c93c4&chksm=8e13a183b964289558908f8238eb17ee3dc050084242d39c32d7de7a5d28098861e11c8fe0c8&scene=21#wechat_redirect)  
