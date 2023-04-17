---
create_date: 2017-12-28T20:51:10 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases:
pagetitle: Power Query 数据丰富，依然轻松搞定！
source: https://mp.weixin.qq.com/s/HvRRRc8DiKstQah5WVTajA
author: 采悟
status: 已完成 
category: 浏览文章 
notes: false
ZK: Origin
uid:
---

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2EQwGOzCiaKHcRz5biajC3fMnSLsywlfa7bCthARS7JcLia2SBBS49tZow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

上一篇文章都是在原表数据基础上的分分合合，但做数据分析的时候还经常需要在原有数据的基础上增加一些辅助数据，比如加入新列、新行，或者从其他表中添加进来更多维度的数据，这些就是数据丰富的过程。

___

01  
**添加列**

Power Query中==添加列有四种形式，重复列、索引列、条件列、自定义列==：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2qBbgPq5DiaBKmJIib9JSxTvD48qJ6s9FY9P1FdVhJVa06gs5iasda2Y0A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**(一)添加重复列**

重复列就是把选中的列复制一列，以便对该列的数据进行处理而不损坏原有列的数据，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2dALIaYReqPoCfkUQ6xxcnvSib8GzjxicKib7hVic5MIwmjrKKt2N3Rw00A/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**(二)添加索引列**

索引列就是为每行增加个序号，记录每一行所在的位置，可以从0或者1开始，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2hMSPiakSbqnxor5WDBuiaDYZ5uPvdNpstAyl2nwQ1oyRSAxbWjbEEGYg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**(三)添加条件列**

添加一列根据指定条件从其他列计算的数据，打开窗口看看，其实就是 if 函数，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG20pxWOrLtPNgwic2CO4mBIibPzymPsDKOlJHtD2vLiaglBh1uoM7gI37eQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

根据上面的条件，得到新的一列，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2xcoxLZtQSS17fA4h0GYdA0l5DPsicyZMqJvCxs8c6reAqbq6WrMSpHQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**(四)添加自定义列**

自定义列就是使用M函数生成新的一列，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2xuCcUlBppicSL2hKY70lX7oLSpQeB9ic3Vyt7hjwdRWqEqYvXVDYTwCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

比如添加一列求1月和2月的和，把两列相加，PQ中的字段用\[ \]框住，不需要手动输入，直接点击右边的字段名就可。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2JjxazJLM1fHCvBT633xKibxAd9tBg6mNmc11rsGusT5ibo412tqXTLlw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

02  
**追加查询**

追加查询是在现有记录的基础上，在下边添加新的行数据，是一种纵向合并，比如有两个表格式相同，需要合并为一个表，点击“追加查询”，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2PU17H1FQsxRt90G0vDgFMpR0ThgGsic5eSInId5dY1nEB4DKKcgzLiag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2FK0ExUZs4dyzTctwfFzBgBXps4p37PJIgTbCNRasvFeSumDzhrGNow/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

03  
**合并查询**

如果说追加查询是纵向合并，那么合并查询就是横向合并，相当于Excel的VLOOKUP功能，就是匹配其他表格中的数据，不过PQ中的合并查询要比VLOOKUP功能强大的多，并且操作也更简单。  

比如我们想从基础信息表中找到每个省市对应的省市和电话区号，点击“合并查询”

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2jg6G7ZpWp88jHiccGvCf65p8cr3ocVhaWFjRMQC7FtNBJ9nYMA8Ju5w/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

选择两个表需要匹配的字段，这两个表都是\[城市\]列，下方联结种类选择左外部：第一个表的所有行，第二个表的匹配行，就得到了下面这张表，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2PEVicVBMhSoF26iblyeHZMomFXXkFanibd270XNynLhdict0eWtgrU8OMQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后点击展开，勾选我们需要的字段，合并查询就完成了，增加了每个城市对应的省份和区号。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNVpUV9OFRY4OaZdiaGjbZG2Hgn5scFepn4P9cEhvyIg3YfJPCXRZ8W3Pu7n5Sj7du90bS1p0LIUTQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过以上的数据丰富以及前面文章中的数据清洗的学习，基本上见识到了所有的界面功能，熟练掌握应该说大部分的数据工作都能够应对，几乎不用任何函数语言。

性价比本来就是Power Query的一大优势，即使不打算学习PowerBI，PQ也值得你抽出几个小时来学习。任何人都可以通过很短时间的练习就可在数据处理上获得突破性的提升，不知不觉间已经站在了Excel的肩膀上。

PQ数据清洗请看：[数据清洗常用的十三招](https://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067158&idx=1&sn=4ad955112df2f40a93b684ed9147f26e&chksm=8e0c7181b97bf89777ae3d9de929867745edcbbfe1f2b396761c0cec716b86ee31e439279add&scene=21#wechat_redirect)  

