---
create_date: 2022-11-16T23:12:42 (UTC +08:00)
tags: wx/pbi/PQ数据处理
aliases: null
pagetitle: 如何利用PowerQuery将特殊文本日期转换为正常日期？
source: https://mp.weixin.qq.com/s/gTmJns8Akjsvw4oCBPVaGQ
author: 采悟
status: 已完成
category: 精读文章
notes: False
ZK: Origin
uid: 
---

当我们将数据导入到PowerQuery时，首先需要<mark style="background: #FF5582A6;">将每个字段调整为正确的类型</mark>，对于日期字段，导入进来时很可能是文本格式，这时就需要先调整为标准的日期类型。  

如果是正常的日期格式，比如下面这两种日期格式：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJdLmuQVzRaicibhNcp9iaqd67RZnqgAnDTRbd125yzpzuoXpwxWbI7ibEFg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

左边是我们常用的"年月日"格式，右边是美式的"月日年"格式，对于这两种文本格式，都可以点击字段名左边的格式符号直接调整为日期型：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJHyJjrX7k39AdoG8dNfuTNLPXp7koU1guOicetC0b8BiaWYHBul2S5rkg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

但是有时也会碰到没法直接调整的情况，以下面这种格式为例：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJMaNv4IF59J3yicMl9XmUtUbNvfvE3W1gET8XxlvS2JBLwV84ibJn0Mkg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这是<mark style="background: #FF5582A6;">英国以及北欧常用的日月年格式的日期</mark>，我们如果按上面的方式直接转换，结果会变成这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJe14M1GPANDBbZ2ucXKh4qdqcnru6Scib49RKmG5dcba2CtMu3dvMHXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

除了第二个日期，其他都报错了，对于第二个日期虽然没有报错，但结果也不正确，本来是2022年8月9日，但转换的结果是2021年9月8日，从这里可以看出，系统还是把这个日期当成"月日年"来转换了，当第一个日期超过12的时候，由于月份不可能超过12的，那么返回的结果就是错误。  

碰到这种格式的日期，怎样才能转换为标准的日期类型呢？介绍三种方法。  

#### **1\. 修改区域设置**

点击字段左侧的类型图表，找到最下面的“使用区域设置”。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJg6w4xxfaYbDC4I6H4n4z5G08bTialiczs1lgoMicMbhxEOTW2r9fe8YzQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后在弹出的窗口中将数据类型修改为"日期"，<mark style="background: #FF5582A6;">区域选择为"英语（英国）"</mark>：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJ0vMWF54DnKkcHeGf1BcM1QEupQfbqvcpUFyGkllQsP72dYXgPicUDAA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过这样的设置以后，这一列的数据类型就调整为正常的日期型了。

#### **2\. 利用Date.FromText的Culture参数**

对于这种转换还可以<mark style="background: #FF5582A6;">使用M函数Date.FromText</mark>，它的第2个参数不要省略，这种格式是英式日期，就可以使用<mark style="background: #FF5582A6;">英国的Culture代码"en-GB"</mark>，添加自定义列：  

> Date.FromText(\[日期\],"en-GB")

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJhm2ia052yU6vicQSzPlqt05WYPw02fzfGykZW0fV1DPibHvAyabvznic6w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这样也可以直接转换成正常的日期。

上面两个方法，需要事先知道这种格式的日期是哪个国家的标准、或者清楚该国家的Culture代码，而很多情况下，我们并不知道这些信息，那么还有下面第三种方法。  

#### **3\. 利用Date.FromText的Format参数**

这个方法同样是是使用Date.FromText添加自定义列，<mark style="background: #FF5582A6;">不过这里使用该函数的Format属性</mark>，写法如下：

> Date.FromText(\[日期\],\[Format="d/M/yyyy"\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJbAkHWEaywDurUanHdCtIymCeM9AhFoliaqqylSqjDiaSvCGicMkgVTibVQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个方法，<mark style="background: #FF5582A6;">无论这个日期格式是哪个标准哪个国家，只要找出日期的规律，把这个日期格式构造出来，利用Format自动识别出其中的年月日信息</mark>。

这里要注意的是，**需要<mark style="background: #FF5582A6;">用大写的M表示月份,不能是小写，因为小写的m表示的是分钟</mark>（minute）**。

并且只要文本中有规律性的年月日信息，哪怕这个日期不是任何一个国家的标准，都可以利用这种方式来转换，比如下面这种格式的日期，用星号分割的日月年信息：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJrcTqTP5n3maB2v1uaRIqzFsDoGic6JrLKgsh0tQ3licbmEiabfmXacicKg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

用上面的前两个方法，无论怎么转换都会报错，但是用第三种方法同样可以轻松转换：  

> Date.FromText(\[日期\],\[Format="d\*M\*yyyy"\])

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPaA0xsBdCLbG062NY10cJJqUaMJdSfYib8rROm7czNEl1GvAXicwXjsT1C1ibV03WOuvEZxCurso1vQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

分隔符是星号，就在Format中构造个以星号分割的日期格式，以便让Date.FromText识别到年月日信息。  

再看一个例子，<mark style="background: #FF5582A6;">八位编码的日月年，同样用这种方式轻松转换</mark>：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJN8tUG6RyvXXy3CkibuibzOHDIw3FiaMw3Gvm5c2ibK7x1Ldc2Hib4BjXPA9icGFib3waEuvplTRr3Ria9RbQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过上面几种方式，就可以处理大多数文本格式的日期了，尤其要熟练使用更普适的第三种方式，对于常规方式无法转换的，都可以尝试用Date.FromText函数来处理。
