---
create_date: 2017-12-23T20:48:57 (UTC +08:00)
tags: wx/pbi/数据处理功能 
aliases:
pagetitle: Power BI与Power Query、Power Pivot 是什么关系？
source: https://mp.weixin.qq.com/s/GeJi_UOfVm3qRJKpX_5hdg
author: PowerBI星球
status: 已完成 
category: 浏览文章 
notes: false
ZK: Origin
uid:
---

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNlXibic6pkkR6ZnBylcJiaMibCcM450QH32iaicEYsPuWFxNe0sjjlKRBMWGW6uIVeLibza3WOt18rCkYWQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

搞不清楚Power BI与Power Query、Power Pivot是什么关系？看这篇文章就够了。

___

刚开始学习PowerBI的时候，总是能碰到Power Query和Power Pivot这两个词（下文简称为PQ和PP)，现在中文里面学习PowerBI的资源本来就不是很多，大部分资源还都是介绍PQ和PP的，那么她们到底和PowerBI是什么关系呢？

微软的很多办公工具都是以Power开头，最熟悉的当然就是PowerPoint了，如果ppt可以直译为超级演示，PQ就是超级查询，PP就是超级透视，我们先来看一下PQ。  

Power Query

用作数据处理的大众化软件就是万人皆知的Excel了，Excel作为日常办公使用当然没有问题，但在大数据时代，她明显有点扛不住，微软也意识到了这一点，所以从Excel2010开始，推出了一个叫Power Query的插件，可以弥补Excel的不足，处理数据的能力边界大大提升，Excel2013也同样可以使用，现在还在用Excel2010和2013的同学可以从微软官网下载powerquery插件使用。  

而到了Excel2016，微软直接把PQ的功能嵌入进来，放在数据选项卡下：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNlXibic6pkkR6ZnBylcJiaMibC14hQbVXpwiaABkzI6SB4xhNlqpFGzHKDeCIo9Pb0mJ70JKMSzo2Xuzg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

PowerBI中的获取数据界面是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNlXibic6pkkR6ZnBylcJiaMibCRkq9KibFF8yXZt2YreuBlxIZgPTffJraN3EIyicIGrb6RZx86xp704Ag/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

是不是非常相似，功能也基本是一样，点击进去后都是进入查询编辑器，所用的也都是M语言，所以学习PP就是学习PowerBI中的数据处理模块，无论在Excel中学还是在Power BI中学，都是一样的。

Power Pivot

接触过Excel的人肯定都知道数据透视表，英文名是Pivot Table，按这个翻译PP可以叫做超级透视，但其功能要比数据透视表强大很多，所以PP被大家称为是数据建模，这个名字一下就显得高大上了吧，不过PP确实名副其实，她被称为微软近20年来最伟大的发明，也是PowerBI的灵魂，PP用到的语言是DAX，以后会详细介绍。

在Excel中也可以使用PP,首先从选项里面把这个功能加载进来：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNlXibic6pkkR6ZnBylcJiaMibCbr2sTcVJDYMvd96E5427a1XE4W7pB3kCl82RWjxWf6UDWxTJbOMCog/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后Excel选项卡下就多了一个Power Pivot，界面如下：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNlXibic6pkkR6ZnBylcJiaMibCrycC1uKNlHejCTnzp5RVo9IbnHDGIPUyaZHc7iaNIiauicxc7Vwic5GZCQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这个和PowerBI中建模选项卡的功能区也非常相似，所以学习PP就是学习Power BI的数据建模，二者的本质内容是一致的。

刚才看Excel选项中加载项的时候，我们看到Power Pivot旁边还有两个Power兄弟，Power View和Power Map，PV就是数据可视化，PM就是数据地图，这两项也已经内嵌到PowerBI中，且功能更加强大。这两个学习都相对比较简单，就不作介绍，我们学习PowerBI的重点就是数据处理和数据建模，学好这两个以后，数据可视化就是水到渠成而已。

**从上面的介绍可以看出，Power Query、Power Pivot、Power view以及Power Map等全部功能聚集到一起，就成了现在的Power BI。**

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNlXibic6pkkR6ZnBylcJiaMibCPtRxzHro629u4PGFwk1G2c7d8IoLVPexnD7ROvsFXJaMJbR1lkx9Sw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

Excel or Power BI Desktop？  

既然在Excel和PowerBI Desktop中都可以学习最核心的组件PP和PQ，那么在哪里学习更好呢，其实都可以，看个人的使用习惯。我个人更推荐直接在PowerBI Desktop中学习，理由如下：

-   PowerBI Desktop界面更友好，逼格更高
    
-   PowerBI Desktop更新速度快，几乎每月都有更新，最新的M函数和DAX函数随时可以调用
    
-   进行数据处理的最终目标是生成可视化报告，发现有趣的见解，这在PowerBI Desktop中整个流程一气呵成，且图表库和便捷性要完爆Excel
    

如果还没有开始学习Power BI，对PP和PQ没有什么概念，这篇文章可能比较枯燥，完全可以先忽略，等有些疑惑的时候再看更好。

