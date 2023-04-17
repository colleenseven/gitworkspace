---
create_date: 2023-03-02T23:30:01 (UTC +08:00)
tags: wx/pbi/DAX函数 
aliases: null
pagetitle: PowerBI数据分析中，如何用DAX计算出有效工作时间？
source: https://mp.weixin.qq.com/s/wSyDb-_5XPqp5u39gzk6PQ
author: 采悟
status: 已完成 
category: 精读文章
notes: False
ZK: Origin
uid: 
---

DAX:: CALCULATE ,MIN,FILTER ,INT,MAX,SWITCH ,HOUR

碰到星友提出的如何计算某个期间的工作时间问题，感觉比较典型，这里分享如下。

比如员工的考勤记录，如果==只有一个开始时间和离开时间，需要扣掉其间的节假日和休息时间，如何统计他们之间的有效工作时间呢==？  

比如下面这个模拟数据：  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMoLIMdlAsqhD8FJAhCgEoCVlnPjicRqWx205X7XwftiarsHohx7DpORDJTAIt6HwhD1xxicr9JGAJ1Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

有两列时间，开始时间和结束时间，要求扣除以下两项后，计算间隔的有效小时数：

-   周末和法定节假日，当天的时间都不统计在内；
    
-   早点9点到下午5点是工作时间，除此之外的时间也不统计在内。
    

也就是说只统计两个时间之间的工作日的工作时间是多少，以小时为单位。  

由于涉及到工作日/节假日的计算，我们首先需要在日期表中做好工作日标记和编号，关于如何做标记，之前已经介绍过，请参考：  

[如何用Power BI进行工作日相关的计算？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077728&idx=1&sn=5d7739914cb98e96b7abd32d402aba3e&chksm=8e13ae77b96427615638ed7351de474f87095c983d3d5c745b94ed1c0fc35a87e34ea247683d&scene=21#wechat_redirect)  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNbtiatk6CdmYgNu9SjpqPtAKbaX23icHwagk7mmSoVQcA7rJzfZgVjyeNKcic1lSFKQHBHAOOvus7Wg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个准备好以后，我们只需要写一个计算列就可以实现，先来看看如何写：

```
间隔工作小时数 = 
VAR A=[开始时间] 
VAR B=[结束时间] 
VAR C=CALCULATE(MIN('日期表'[工作日编号]),FILTER('日期表','日期表'[日期]>=INT(A)&&[工作日标记]=1)) //找出晚于开始日期并且是工作日的最小的工作日编号
VAR D=CALCULATE(MAX('日期表'[工作日编号]),FILTER('日期表','日期表'[日期]<=INT(B)&&[工作日标记]=1)) //找出早于结束日期并且是工作日的最大的工作日编号
VAR E=CALCULATE(MIN('日期表'[工作日编号]),'日期表'[日期]=INT(A)) 
VAR F=CALCULATE(MIN('日期表'[工作日编号]),'日期表'[日期]=INT(B))

VAR G=IF( E+F=0 , D-C+1 , D-C )*8  

VAR H=                        
    SWITCH(
        TRUE(),
        E+F=0,0,
        F=0,17-MAX(HOUR(A),9),
        E=0,MIN(HOUR(B),17)-9,
        MIN(HOUR(B),17)-MAX(HOUR(A),9)
    )

RETURN G+H
```



结果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMoLIMdlAsqhD8FJAhCgEoCUEsXEnlicb2hLDBGvJD4DANT9KfX02mEia1kTiaEot4LZ778YiakNDSR4g/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

这个逻辑是通过变量一步步实现的，理解里每个变量的逻辑，整体的逻辑也就基本理解了：  

A：获取本行的开始时间  

B：获取本行的结束时间

C：找出晚于开始日期并且是工作日的最小的工作日编号

D：找出早于结束日期并且是工作日的最大的工作日编号

E：计算开始日期当天的工作日编号

F：计算结束日期当天的工作日编号

G：两个时间之间的完整工作日的天数\*每天工作8小时

H：开始日期和结束日期当天的工作小时数

其中关键是如何找出当天日期对应的工作日编号以及最近的工作日的编号，其中的逻辑并不复杂，用到的函数也很简单，但是需要对每个日期进行细致的判断和分析，最终通过简单的运算得到需要的结果。  

这种计算也不要指望看到这个公式立即就明白，最好是自己拿几个时间动手练习一下，想清楚工作时间的业务逻辑，思考如果开始日期或者结束日期是否为节假日等各种情况，分别应该如何计算，这样才能真正的去理解掌握。

感觉我写的这个公式比较繁琐，如果你有更简洁的写法，欢迎留言分享，如果可以更简单实现，赠送PowerBI领域图书一本。
