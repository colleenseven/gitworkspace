---
notes: False
aliases: null
create_date: 2022-09-25T23:25:04 (UTC +08:00)
tags: wx/pbi/数据处理功能
pagetitle: PowerBI报告中莫名冒出来的筛选器，是怎么回事？
source: https://mp.weixin.qq.com/s/MWtPHFT1QHVhOG0EDndrEg
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

PowerBI中的筛选器，是个非常基础的功能，使用起来也很简单，我们经常会用到，之前也专门介绍过它的用法：  

[学会使用PowerBI报表中的筛选器](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067724&idx=1&sn=a0140bb47a2fe5d9058f80d1d5e8eb36&chksm=8e0c775bb97bfe4d8d672ad8e1dfbca96d0bd8dddb6f51c92f7ad912d890b6a6f82a93658da1&scene=21#wechat_redirect)  

[Power BI的新筛选器，有两个亮点！](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068230&idx=1&sn=ada06efa4c597b06ee8ebbf0a6667895&chksm=8e0c7551b97bfc47ff432182e29e91873d32d830036f89d5daee5604f072d895a4fb13ca5bed&scene=21#wechat_redirect)  

不过在筛选器窗格中，有几种特殊的情况，经常被人问到，自己明明是没有添加筛选器的，却在筛选器面板中突然冒出来了某个字段的筛选器，并且可能还删除不掉，这是怎么回事呢？  

下面介绍3个常见的非手动添加的筛选器情况。

**1\. “包括”和“排除”筛选器**

在图表中，<mark style="background: #FF5582A6;">鼠标右键菜单有两个功能“包括”和“排除</mark>”，

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMucXInVVsJkvBiaichaT4gV5EicxrksQ855JiapNHOYqLojRJg6ZlOxnEZ2uWibJzfVD9UxicytqmhI6Zg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

通过这两个功能，可以很方便的进行视图操作，比如鼠标放到2020年那一行，右键“排除”，就会把这一行筛选出去，只保留其他行。  

但是排除之后，很多人不知道怎么<mark style="background: #FF5582A6;">重新显示全部数据</mark>，其实这个操作是在筛选器里：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMucXInVVsJkvBiaichaT4gV5uTd4FLkLImkI6jkMcZDxCXyP5lF2EY6hSMiaxxt5AqRK6RLObMxJcoQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个筛选器是通过上面的操作自动生成的，如果想<mark style="background: #FF5582A6;">撤销排除</mark>的效果，直接在筛选器里<mark style="background: #FF5582A6;">把这个“已排除”筛选删除即可</mark>。  

右键中“包括”的功能以及撤销的操作同上。

**2\. 向下钻取筛选器**

你可能在筛选器中见过下面的这种，斜体字：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMucXInVVsJkvBiaichaT4gV5uNR1rjRWoSg3jucpLiamhy1GhkBn33bEEw1c59kMv6iby4BPMsCLhW2g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种是<mark style="background: #FF5582A6;">向下钻取的筛选器</mark>，是因为该图表有层级，并做了向下钻取的动作：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMzwI6kZESsshdRAfbCno49ADpYoicPR5c3Rsu6RNO85NLIpicuRm8xRXXQPwQ61FTDLbNN2RqmGhxA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于表格的钻取，可参考：[玩转PowerBI中的「表格」](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067625&idx=1&sn=6d48553aea3bc7baffecedb3d23af924&chksm=8e0c77feb97bfee877dfcdce78764746dd24f445b3bc6fd43c964a99eb08839983ad4b98f614&scene=21#wechat_redirect)  

如果再向下钻取，还会出现季度名称的筛选器；<mark style="background: #FF5582A6;">这种筛选器不能手动删除，后续再进行向上钻取的操作后，这些筛选器也会自动消失。</mark>

**3\. 交叉钻取筛选器**

上面的<mark style="background: #FF5582A6;">向下钻取筛选器，无法删除，但是可以编辑</mark>，可重新筛选其他项目，但是还有一种筛选器，既<mark style="background: #FF5582A6;">无法删除也无法编辑</mark>，那就是<mark style="background: #FF5582A6;">交叉筛选筛选器</mark>。

这种筛选器是<mark style="background: #FF5582A6;">向下钻取筛选器连带出来的</mark>，如果<mark style="background: #FF5582A6;">向下钻取筛选器通过交叉筛选功能传递到报表页上的另一个视觉对象，交叉钻取筛选器就会自动添加到窗格中</mark>。

假如上面的矩阵向下钻取到2021年时，该页还有一个柱形图，则选中这个柱形图，就会发现这个柱形图的筛选器中就有个2021的筛选器：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJOV3akiaEDkTYS3cKekjjnJeF3d77l1YSKU55QzNxw5fXbhic5L9BBrVlfFPFdVDAovgF36c13D8V1Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个筛选器无法做任何操作，想删除也删除不掉，那如果必须删除应该怎么办呢？  

既然这个筛选器是由其他图表的向下钻取导致的，那么对钻取的图表进行向上钻取，就可以自动清除这个筛选器。

以上就是三个比较特殊的自动生成的筛选器，看完本文后，如果你再遇到这种情况，应该就清楚它们是怎么来的、以及怎么应对了。
