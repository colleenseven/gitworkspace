---
create_date: 2022-12-19T23:48:17 (UTC +08:00)
tags: wx/pbi/DAX函数 
aliases: null
pagetitle: Power BI本月正式推出的DAX新函数：OFFSET、INDEX、WINDOW
source: https://mp.weixin.qq.com/s/4LehwUjEAzCv7ACk_Zt5Fg
author: 采悟
status: 已完成
category: 精读文章 
notes: False
ZK: Origin
uid: 
---

DAX:: CALCULATE , OFFSET, ALLSELECTED ,INDEX,WINDOW ,ABS,

2022年的最后一次更新，正式发布了三个新的DAX函数，OFFSET、INDEX、WINDOW，这篇文章来看一下这三个函数的用法。

**OFFSET**

用于检索偏移特定行后的结果，语法如下：  

> OFFSET(
> 
>    偏移的行数，//可以是常量，也可以是返回值的表达式
> 
>    表表达式，//可选
> 
>    orderBy，  //可选，排序依据,如省略,第二个参数须指定
> 
>    空白参数， //可选，保留的参数位置,暂时无用
> 
>    partitionBy // 可选，分区依据，如果省略，视同只有一个分区
> 
> ）

语法看起来比较复杂，通过具体的示例来理解，可以更轻松地熟悉它的用法。

下面根据这个表格来说明，这是每个季度的销售额，
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6UktMMraLVsdUmrgJ16YrAOibicatSuZQkvwibwRPvnf6xGwF9iaCHDTzMub7SjpcxqFBUICJ7DEegg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6UktMMraLVsdUmrgJ16YrAOibicatSuZQkvwibwRPvnf6xGwF9iaCHDTzMub7SjpcxqFBUICJ7DEegg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果要获得上个季度的销售额，除了用之前的时间智能函数，还可以这样写：

> OFFSET =
> 
>  CALCULATE(
> 
>      \[销售额\],
> 
>      **OFFSET(-1,ALLSELECTED('日期表'\[年度季度\]))**
> 
> )

OFFSET返回表，度量值中一般利用CALCULATE来返回定位后的结果（下面两个函数同样如此）。

这里就是只用了OFFSET的前2个参数，第一个参数-1，表示提取向前偏移1行的数据（如果是向后偏移2行，取下下个季度的值，第一个参数应该是2）；第二个参数是输出的行，后面的参数都可以省略，结果如下：
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6UktMMraLVsdUmrgJ16YrXgQ2et4tX4EBRCOQjNIqCJfKRREbJ8iaVskC8qw9ibXmslYKSibia5Cf6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6UktMMraLVsdUmrgJ16YrXgQ2et4tX4EBRCOQjNIqCJfKRREbJ8iaVskC8qw9ibXmslYKSibia5Cf6g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
第3个参数ORDERBY省略，默认按照第二个参数列排序，也就是按年度季度排序，向前偏移一行，就得到了上个季度的数据。

如果想在每年范围内进行这样的偏移计算，就需要用到最后一个参数，度量值这样写：

> OFFSET =
> 
>  CALCULATE(
> 
>      \[销售额\],
> 
>      **OFFSET(  
>         -1,**
> 
>         **ALLSELECTED('日期表'\[年度季度\],'日期表'\[年度\]),,,**
> 
>         **PARTITIONBY('日期表'\[年度\])**
> 
>     **)**
> 
> )

**对于==在PARTITIONBY中的字段（以及在ORDERBY中的字段），必须放到第二个参数中**==，这就是上面度量值中，第二个参数里面也要带上'日期表'\[年度\]的原因，在年度内偏移的效果如下：  
![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6UktMMraLVsdUmrgJ16YrZdE5JpcdTN0wWGcQd6vn3uoEJHMoSHTA6f6fLvaa4oRp7XsFd6efSg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6UktMMraLVsdUmrgJ16YrZdE5JpcdTN0wWGcQd6vn3uoEJHMoSHTA6f6fLvaa4oRp7XsFd6efSg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
这种偏移只在年度的区间内进行，年度变化后，再重新取开始，所以第一个季度都是空值。

**INDEX**

用于检索特定行的结果，语法如下：

> INDEX(
> 
>    检索位置， //1表示第一行，-1表示最后一行，以此类推
> 
>    表表达式，//可选
> 
>    orderBy，//可选，排序依据,如省略,第二个参数须指定
> 
>    空白参数， //可选，保留的参数位置,暂时无用
> 
>    partitionBy // 可选，分区依据，如果省略，视同只有一个分区
> 
> ）

它和OFFSET的参数几乎一样，还是拿上面的例子来说明这个函数的用法。这样写：  

> INDEX =
> 
> CALCULATE(
> 
>     \[销售额\],
> 
>     **INDEX(1,ALLSELECTED('日期表'\[年度季度\]))**
> 
> )


![https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOWhJpSeIXQDicfszJJ7y5ic0A2SFB8UPyhZBHicOtTVUymINtibCCJsiac0YV1safAyZ6K4pT4AANnwJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOWhJpSeIXQDicfszJJ7y5ic0A2SFB8UPyhZBHicOtTVUymINtibCCJsiac0YV1safAyZ6K4pT4AANnwJg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)
如果要返回第一个季度的数据，度量值

可以看出它全部返回的都是第一行的数据；如果想按年度返回本年第一季度的数据，同样可以利用最后一个partitionBy参数：

> INDEX =
> 
> CALCULATE(
> 
>     \[销售额\],
> 
>     **INDEX(  
>         1,**
> 
>         **ALLSELECTED('日期表'\[年度季度\],'日期表'\[年度\]),,,**
> 
>         **PARTITIONBY('日期表'\[年度\])**
> 
>     **)**
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOWhJpSeIXQDicfszJJ7y5ic0qG5qGmRicT45CjgDVEP7ufAJ7DFjW8mxpQ4je0pAiaS1UVxyvATPBnww/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

每一行的结果都是本年第一季度的数据。  

**WINDOW**

返回位于给定区间内的多个行，语法如下：

> WINDOW(
> 
>    起始位置， 
> 
>    起始位置类型，//可选， ABS（绝对）和 REL（相对），默认为 REL
> 
>    结束位置，
> 
>    结束位置类型，//可选， ABS（绝对）和 REL（相对），默认为 REL
> 
>    表表达式，     //可选
> 
>    orderBy，  //可选，排序依据,如省略,第5个参数须指定
> 
>    空白参数，//可选，保留的参数位置,暂时无用
> 
>    partitionBy  // 可选，分区依据，如果省略，视同只有一个分区
> 
> ）

后面4个参数与前两个函数也是一样的，只是WINDOW返回一个区间，所以前面用了4个参数来确定起止位置以及位置的类型。

常用的==滚动就和，比如计算前两个季度的累计之和==，可以用WINDOW函数这样写度量值：

> WINDOW=
> 
> CALCULATE(
> 
>     \[销售额\],
> 
>     **WINDOW(**
> 
>         **-1,REL,0,REL,**
> 
>         **ALLSELECTED('日期表'\[年度季度\])**
> 
>     **)**
> 
> )

如果位置类型是相对，则==位置负数就表示向前移动几行，0表示当前行==，效果如下：

如果==将位置改成绝对，1就表示表的第一行（-1表示表的最后一行）==，度量值这样写：

> WINDOW =
> 
> CALCULATE(
> 
>     \[销售额\],
> 
>     **WINDOW(**
> 
>         **1,ABS,1,ABS,**
> 
>         **ALLSELECTED('日期表'\[年度季度\])**
> 
>     **)**
> 
> )

起止位置都是第一行，其效果就是取绝对位置的第一行数据：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6UktMMraLVsdUmrgJ16Yrf9j1YwRicaEFiaoJWz2lAzgs9wFTIYRuuyQ9Yy4lB5mNIZM80aNbr6IA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

还可以通过设置起始位置绝对引用，结束位置相对引用，来实现累计求和的效果：

> WINDOW =
> 
> CALCULATE(
> 
>     \[销售额\],
> 
>     **WINDOW(**
> 
>         **1,ABS,0,REL,**
> 
>         **ALLSELECTED('日期表'\[年度季度\])**
> 
>     **)**
> 
> )

起始位置1绝对，就是从第1行开始，结束位置0相对，就是到达当前行结束，因此可以实现==从第一行累加到当前行的效果。==

看到WINDOW函数的起止位置设置，是不是有==Excel单元格绝对引用、相对引用的感觉，它确实像Excel一样，带来了更加灵活的区间计算==。

WINDOW函数像前面两个函数一样，也可以设置最后一个partitionBy参数，==来实现本年内的区域计算，比如本年累积求和==：

> WINDOW =
> 
> CALCULATE(
> 
>     \[销售额\],
> 
>     **WINDOW(**
> 
>         **1,ABS,0,REL,**
> 
>         **ALLSELECTED('日期表'\[年度季度\],'日期表'\[年度\]),,,PARTITIONBY('日期表'\[年度\])**
> 
>     **)**
> 
> )

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJM6UktMMraLVsdUmrgJ16Yrn5PXic73DDpmNFYj3kMFGicoKGoWprGD693ltFn6EWugrOoPu5t385kg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上就是这三个新函数的基本用法，为便于理解，上面的示例用的是日期序列计算，其实熟悉了他们的用法以后，其他类型的计算也是可以用这些函数。

这三个函数还没有最终完善，相信之后它们会变得更加强大和灵活，也会带来更丰富的应用场景。
