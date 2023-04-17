---
create_date: 2023-01-12T23:34:59 (UTC +08:00)
tags: wx/pbi/可视化图表 
aliases: null
pagetitle: 使用Power BI制作个性的凸凹图
source: https://mp.weixin.qq.com/s/OxM82AeXglLOprmRiq88-Q
author: 采悟
status: 已完成
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

有星友最近浏览到下面这个图，感觉很清晰，问这是哪个图表？PowerBI能不能做出来？  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia20uUItV4ASb6Zqn3Qr3oia9zca9ia5WScXnEVtsPvuKOJZrKMuuh3aJXQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

它看起来像是折线图，其实它正式的名称是==凸凹图（Bump chart），常用来呈现多个类别随时间变动的排名情况。==

虽然PowerBI没有完全对应的图表类型，不过也并不难制作，因为它就是折线图的一种变体，==当数据是相对排名而不是绝对数据时，用折线图可以轻松实现这种凸凹图的效果。==

以上图中的数据为例，

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia2FtowX0Ec5arPeWWf3cMic9sJA4eTVn4MEibWr5W6DPco7AibnpqC36iaBw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

首先用这三个字段生成一个折线图，字段拖拽进去默认的效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia2lIaq5nKhOL29zMiawibMlvNbia3629Ic7pUxjaIUiaia9oUcGLbtMO1iawsw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

下面就通过折线图的各项格式调整，来看看PowerBI如何将这个折线图变成凸凹图的果。  

**调整标题**

折线图的标题默认是字段的聚合方式，看起来比较扎眼，这里就先把它调整过来，调整方式如下图。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia2nDQ0E2koYhp4CY9fs8EuGjibPT9CdRHGrPrERG3ZyoW19apIHHlhNWg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于格式调整，并没有一定的顺序，只要将每个元素的格式调整成满意的效果就好。  

**调整X轴**

当X轴的字段为数值型时，默认是连续型，不会全部显示出来。所以上图看到的X轴只有部分年度，并且显示的也与实际数据不符，为了让X轴正确的全部显示出来，将类型更改为“类别”就可以了。

X轴标题关掉。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia2fcVX0xM1Ric7Do7OP1oPCHLECokozTlITxJ8SAsJicBfesQy59TiaOzbA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**调整Y轴**

Y轴默认从上到下是降序排列的，也就是越往上数值越大，但是对于排名来说，应该是升序排列，最上面是第1名，所以打开“反转范围”选项。  

另外，将Y轴的显示刻度切换到右侧，可以打开“切换轴位置”选项。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJODeaHrHu8fuHjNgceqDMyC2TM0MesU2p3lqnDO9lzwicHYcibLQhyn0L9rib6R2LCuI5EibaAMTIc0uw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

Y轴的标题同样也关掉。

**去掉图例/添加序列标签**

这里不用图例，直接将每个城市显示在折线图末端，就可以打开“序列标签”，并将序列位置设置在“左”侧。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia2icLGIBLuMibuicAicibVfnTQyuNInwLoLt11DEOCeoA3u71wibECHUic0fVmw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

**添加标记/调细折线**

凸凹图关键是要突出标记点，打开“标记”，设置形状为圆点，大小调整到6。  

![https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia2GdJI0f8Yicqbn2w3z41q1UDX4dJ2jIyPdeH4guaVsVSo2iacWt5Mop7A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia2GdJI0f8Yicqbn2w3z41q1UDX4dJ2jIyPdeH4guaVsVSo2iacWt5Mop7A/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

折线笔画宽度调细，这里调整为1（笔画宽度最小可以调整到0，这时折线就不再显示，只有数据点了）。

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia2BoZSNUcDTdfa7nIvF3Oden2qdpH9nREyHSp09weNMUYNInAj3lUWBA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

到此已经基本上做出凸凹图的效果，不过还有个小问题，就是最上面和最下面两行的标记都只显示一半，没有完全显示出来，对于这种情况，可以再调整一下Y轴的范围。

**微调Y轴范围**

Y轴默认是从数据的最小值到最大值，为了让这两个地方的圆点全部显示，可以手动微调一下，比如从0.9到8.1，就可以全部显示出来了。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJODeaHrHu8fuHjNgceqDMyC2W2HHesjnqqoK1gxLkD0ibibQqG2VxFpKc0Jr4dxq0LWzlHr52icaQ5CA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

关于Y轴范围的调整，如果数据是不确定的，也可以通过DAX写好度量值，来进行动态的调整。

至此主要的格式调整完整，最终效果如下：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNXYEbWDsftByzY8vbHpKia2Rq2tR389rlg2SMKgRbxvsxhtcnGib4e4WlWDOxib2798ND6qX2rlQDgw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

其他细节，如字体的大小、折线的颜色等你都可以根据需要来自定调整，除了数据点标记无法调成空心的圆点、Y轴刻度值没有圆形的图标之外，其他的细节基本和原图一致了。  

以上就是在PowerBI中凸凹图的做法，实现起来很简单，关键是要清楚折线图的各项格式设置，进行灵活的调整。

通过模拟凸凹图的制作，你对折线图的各项设置是不是也更熟悉了呢？  
