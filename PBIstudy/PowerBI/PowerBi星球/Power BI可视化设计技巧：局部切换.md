---
ZK: Origin
notes: False
aliases: null
create_date: 2022-05-07T11:51:51 (UTC +08:00)
tags: wx/pbi/可视化方法
pagetitle: Power BI可视化设计技巧：局部切换
source: https://mp.weixin.qq.com/s/CscEOMpZUo5F0rfJ4MtGRg
author: 采悟
status: 已完成
category: 浏览文章
uid: 
---

[上篇文章](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080023&idx=1&sn=001ead7e1723917c204db70d6f198425&chksm=8e13a740b9642e5620efbd3bfecfc47c3b33062715dc6d5e48f033010fb815a07ee090c8fb52&scene=21#wechat_redirect)介绍了[页内导航](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484080023&idx=1&sn=001ead7e1723917c204db70d6f198425&chksm=8e13a740b9642e5620efbd3bfecfc47c3b33062715dc6d5e48f033010fb815a07ee090c8fb52&scene=21#wechat_redirect)，其实我们还可以进一步设计，在一页中制作两个页内导航，除了前面的按日期粒度切换图表数据，另外制作了动态切换收入、利润变动的整体趋势，如下图。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOw9BKOEkR7xE1eRLoPOibBVBb7UR8O1OSoBejoxa394vkicZoM9CnibFEQbEepAibaFYW7euVMpYvjA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

关于下层导航的制作，与上层导航的制作方法一致，前面已经介绍，这里不再重复。不过如果你设计这种导航，很可能会面临这个问题：**<mark style="background: #FF5582A6;">同一个页面上的两种导航会相互影响，不能独立切换</mark>。**

比如下面的导航再切换到利润趋势时，上面的导航也自动变回到本月的数据；而上面的导航切换时，下面的图表也自动变回到收入趋势。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMOw9BKOEkR7xE1eRLoPOibBbSTQagYt3VJgVjXheus0vojfDI0eNuTuAt4vQFqJC0ZQNqBPOrv0QQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

如何让这一页内的两种导航相互独立，点击按钮只切换相关的图表，而不影响到其他可视化对象呢？

这就是本文要介绍的**<mark style="background: #FF5582A6;">局部切换</mark>**，专门来解决这个问题。

下面来看看局部切换的的设计思路和步骤。

**准备工作：视觉对象分组**  

为了对两个切换所涉及到的可视化元素进行区分和管理，以便进行后续的操作，首先需要对这些可视化元素进行分组。

打开选择面板，里面显示的就是本页报告上的所有可视化元素：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOw9BKOEkR7xE1eRLoPOibBpjIgtGWn0DXSUtKFUXXZ56QUt0F6yYgDW6tqksFvfEU03BvdlHsWAQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

对于每一个视觉对象，应该养成重命名并排序的习惯，并将同一个模块的元素放到一起。  

然后就可以<mark style="background: #FF5582A6;">将上层导航涉及到的全部可视化对象组合到一起</mark>，选中第一个，然后按住shift键选中最后一个，即可批量选择，然后右键>分组，如下图：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOw9BKOEkR7xE1eRLoPOibBUN3p40UNYSqZSmPJt6ZbPvfsYQEyEemZKlSYaDcAvPuteIBmHtS9hQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

分组以后，还可以对这个<mark style="background: #FF5582A6;">分组重命名</mark>，这里重命名为“本期”。  

同样的方式，对下层导航涉及的这几个可视化元素分组，<mark style="background: #FF5582A6;">命名为“趋势”</mark>，分组后的效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOw9BKOEkR7xE1eRLoPOibBndkrUL2EsiawwCLgAUk6Z0PHGupbJxiaibbib4q8PKiaF2Qdw3517YH8kvA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

分组完成以后，就可以进行下面的操作了。

**<mark style="background: #FF5582A6;">局部切换设计：调整书签属性</mark>**

这是最核心的一步，通过<mark style="background: #FF5582A6;">调整书签的属性，让书签只作用于所选择的视觉对象</mark>。

打开书签面板，需要对之前建好的书签，进行逐个调整，这里主要以第一个书签“本月”为例，介绍调整的方法和步骤。

#### **1、调整书签属性为“所选的视觉对象”**

选中“本月”书签，然后在选择面板中**选中本期**（这就是前面分组的好处，可以非常方便的选择本书签需要作用的视觉对象），右键书签，勾选“所选视觉对象”：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMOw9BKOEkR7xE1eRLoPOibBjH2320ibeTQLyvAC9blvZ9nJLCYia6rx8Jn4ibCICz2eR4iaqUW8KAgDlA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

#### **2、更新书签**  

再次右键书签，点击“更新”，这样关于“本月”的书签设置完成。  

#### **3、重复前2个步骤，调整其他书签**

同样的方式，调整剩余4个书签的属性。

对于下层的趋势导航模块，也是同样的操作，不过在进行第1步操作时，要选择的是“趋势”组合。

然后就实现了局部切换的效果。

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMOw9BKOEkR7xE1eRLoPOibBMtHJnOTsht13vTIHVHRXj4Kg26QDqwoibGwpbTl3CNIRtJPy8Yx6XhQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

上层的切换和下面的切换完全独立，相互不影响，很自然的实现了在一个页面中，动态展现多类别、多图表的需求。

关于书签，涉及的都是非常细节的操作，多动手多实践，才能够灵活运用，精准控制，更多书签的应用场景参考：

[Power BI书签的各种属性](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484078084&idx=1&sn=ab69796a96590211deaf842b188a63b2&chksm=8e13acd3b96425c5f34d50c390caedac3a0c57559ac0cb1ecce6394263c7ad9805331a08afc5&scene=21#wechat_redirect)  

[Power BI书签的十大经典应用](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068940&idx=1&sn=723666f112f15b6d20fcd980d2268c97&chksm=8e0c489bb97bc18d87c357cd2ee31a363f2146dcfdac61a32e8708a6ecf5e502370210925251&scene=21#wechat_redirect)  
