---
create_date: 2022-12-31T00:07:28 (UTC +08:00)
tags: wx/pbi/可视化图表 
aliases: null
pagetitle: Power BI SVG地图应用总结-2022版
source: https://mp.weixin.qq.com/s/T_X_PC6xwvqXowDplBrl4g
author: wujunmin
status: 已完成 
category: 浏览文章 
notes: False
ZK: Origin
uid: 
---

2022的其它总结：

[零售书籍Top10-2022版](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491268&idx=1&sn=4135f38418c1912e6c13c4d09decc1df&chksm=97db2794a0acae82629ec6c7a193068c07a549893063d021c061aa6187fef7f206ee3aa8d1eb&scene=21#wechat_redirect)  

[Power BI模拟大厂图表总结贴-2022版](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491403&idx=1&sn=b868c0fc4b935aaba5f3490533cfb5c9&chksm=97db261ba0acaf0d717007b39c83e1dfa5a6a995bc1abaf778faa15981ec11139a4fd8b291b6&scene=21#wechat_redirect)  

_申明：本公众号提到的地图仅供个人学习_  

___

近年我比较了Power BI不同类型地图的优劣，从实用性和可扩展性结合，最后选择==SVG地图作为主要研究对象==。2022年也取得了一点成果，本文是一个总结。  

**1\. SVG视觉对象及应用情景**  

___

Power BI显示SVG着色地图常用的视觉对象有三个，内置表格/矩阵、Synoptic Panel和HTML Content。

后两个需要在图表市场下载，如果没有Power BI账号可以参考本文无账号的下载方式：[无Power BI账号，如何下载并使用图表市场的第三方图表？](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488194&idx=1&sn=430a274df5e22d859b5907f4bb2982c7&chksm=97db2b92a0aca284235757426d0b7e5ee6f48b6716e76fa62ba3ffab3376b691f1542e35e9d4&scene=21#wechat_redirect)  

内置表格/矩阵用来显示迷你地图，《[表格/矩阵展示迷你着色地图](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247487138&idx=1&sn=99860302694be5b3708e40d7889f90a9&chksm=97db37f2a0acbee4933fd300796874e21830c31d8327ea4e0ad002f43b0e48c88edc6e4a0b77&scene=21#wechat_redirect)》这篇文章介绍了详细操作方式。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RBPe2miaDQAibZ8PeGwEdjEX4MbtsXhY1SvJm1PicmZhiabQ6XlvhK7m2JmDMwNdI2Fytb14CU9Ee2IA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

==Synoptic Panel是最主要的Power BI SVG着色地图载体==，各个层级都可以使用。《[Power BI Synoptic Panel显示着色地图](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488025&idx=1&sn=d2200a158b4edd501c78173fdfd29f8e&chksm=97db2b49a0aca25f7b600d2e9a0036df1e48c642359be95e7a5f4add9fd93dc40d5b85a258c4&scene=21#wechat_redirect)》这个视频介绍了该视觉对象的详细用法。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RBPe2miaDQAibZ8PeGwEdjEXP7ic4mLMeW5GyAjRPkK25dV1eNKwwl5dQUSnWo00o58udRj7sJBSmyw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

HTML Content主要用在高阶的SVG地图用法，牵扯地图代码重构，后续会讲到。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RBPe2miaDQAibZ8PeGwEdjEXVYWdfFHkEGNia0WGs92atZ9Pa8fDic4MFNyjELCKF1lotRc3kxtgbnqQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**2\. 不同层级的SVG地图下载及使用**  

___

**全球或者其他国家/地区**，推荐amcharts和mapsvg这两个地图资源。使用时需要注意从地图中提取ID作为与Power BI数据关联的载体。《[Power BI 各国/地区 SVG着色地图下载及使用](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247489221&idx=1&sn=2ac6d5a53e972fbe018bd9adaab394fa&chksm=97db2f95a0aca68313be707fd0729f0879ba9f4b78f84c36dfbcfce0b31a2dc8541552e959c6&scene=21#wechat_redirect)》以mapsvg为例视频讲解了如何操作。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RBPe2miaDQAibZ8PeGwEdjEX6jKbvibdgBBZKn53M2tua6nygFbJqJdKKoxy4x71pLo6dFf3UQgxYPA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**全国以及省到市**的地图资源可在公众号后台回复"SVG地图"获取相应下载链接。该资源的ID是地理位置的拼音，Power BI设置方式参考这个视频《[Power BI Synoptic Panel显示着色地图](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488025&idx=1&sn=d2200a158b4edd501c78173fdfd29f8e&chksm=97db2b49a0aca25f7b600d2e9a0036df1e48c642359be95e7a5f4add9fd93dc40d5b85a258c4&scene=21#wechat_redirect)》

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RBPe2miaDQAibZ8PeGwEdjEXZLHppjEWIPSqMZQMIKzegPUPDIXeumKsHBcQJqAnl3fT5W3esMulbw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**市到区县**，以下视频介绍了两个地图资源，并以温州市为例讲解如何应用到Power BI。

以下视频是另外一个NB的省市区县地图资源：  

**区县到乡镇街道村**在网上很难找到现成的SVG资源，需要自己制作。可以使用阿里云地图工具（以上视频有介绍）的边界生成器，对乡镇街道村进行自行框选，并导出SVG格式。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RBPe2miaDQAibZ8PeGwEdjEXWcBrLTXM9dm8TjXFcwHicV2SzyuXzKmuLLPb4H2Iia3OJFVILUB5T9Pg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

这种方式有个巨大的BUG，就是你可能对所在的省份、城市的地图形状很熟悉，但是对所在的区、街道、村的形状可能非常茫然。比方下图是温州市瓯海区的形状，一般人很难有认知。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RBPe2miaDQAibZ8PeGwEdjEXunHIpt8Y7WBTMicOfiaHP9V1NAwndYgmG8FaE4dtkZ5FjMJcqbIm9bkw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

因此，对区县以下层级建议的方式是，PPT中放一个当地的地图底纹，然后将地理的位置画个圈，类似下图中的商圈。详细操作可参考此文《[货品极端尺码商圈分析](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247486899&idx=1&sn=3862463efb9bc3e4a6d25dc6d7b8e093&chksm=97db34e3a0acbdf537d508ed333eb47f1078e7f2bc60fcaa36c87ec207c2f24aabbd3139236a&scene=21#wechat_redirect)》，对这些层级，人们更容易在真实的地图上感知其位置。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RBPe2miaDQAibZ8PeGwEdjEXvX35lhKcwWhFhPAyPoTM8DIOfVR9YWgZfxfH1b7OfqxEhl1t1xUJZQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**再下一级到建筑物**，人们对建筑物的内部空间形状反而比乡镇街道熟悉，可参考[此文](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247484811&idx=1&sn=46dbd2d67473d39adb02d79ed1c4e5e6&chksm=97db3cdba0acb5cd39f73f27ab6bb0a6ee64da377e4de9fc329d7a58a0be918eebb7331e1a6d&scene=21#wechat_redirect)后半段进行建筑物布局的勾勒。下图是一个商场的布局，商场内部再细分到一个店铺内部的布局，操作方式是一样的。

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6RBPe2miaDQAibZ8PeGwEdjEXc1IsLFYib8XHHvK7Q8rfD1XaCpsniaAJw9a558GPeJFQVACThs5LAKJQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

**3\. 地图区域组合与拆分**

___

有些读者可能有**大区划分**需求，比方跨国公司可能将全球分为北美、亚太、非洲等等，国内划分为东区、西区、南区北区，某个省内进行跨城市划区管理。

《[Power BI 如何自定义着色地图的大区？](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488222&idx=1&sn=bd5328ca401d9de5286bdb71eb3abfee&chksm=97db2b8ea0aca298c5ebf97762845019e6e529c9af4ad7ba3ceeafc4d46035b12aebe2366566&scene=21#wechat_redirect)》讲解了如何进行SVG地图的大区划分，如读者有需要《[Power BI JSON地图如何自定义区域组合](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488382&idx=1&sn=0532e2d61c7978d439560051207a6a37&chksm=97db2a2ea0aca3380916dcbe9b82ab0635744cf1ee55d343ce1b77299972cd7ce1fa184a0836&scene=21#wechat_redirect)》讲解了JSON地图的大区组合方式。  

还有读者可能有**跨层级地图展示**的需求，比如业务非常分散，温州市、西安市、大连市有业务。在全国地图上直接按省份标注显得自欺欺人，因此有在全国地图标注城市的需求。《[Power BI制作跨层级跨地区着色地图](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488752&idx=1&sn=6a0fd35f1f01267b48e15852e61cd5ad&chksm=97db2da0a0aca4b623ec699f547a63bf5b693cc48b92d91c37efb81a000dec3cd81a55866abb&scene=21#wechat_redirect)》这篇文章解决了这一问题。

**4\. 地图细节优化**  

___

以上操作方式大都使用了地理的拼音作为ID与Power BI连接，因此需要数据源中准备拼音列。能不能**直接识别中文地理名称**？《[Power BI着色地图优化中文地理标签](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488452&idx=1&sn=b71b0d20ece1dc8f87f6259df62b290b&chksm=97db2a94a0aca382b66ee46b7ca20bb27ca32dcfa933c39ef148ab0ab2aa46b32ee4541ce2c9&scene=21#wechat_redirect)》提供了解决方案。

 [Synoptic Panel](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488025&idx=1&sn=d2200a158b4edd501c78173fdfd29f8e&chksm=97db2b49a0aca25f7b600d2e9a0036df1e48c642359be95e7a5f4add9fd93dc40d5b85a258c4&scene=21#wechat_redirect)是Power BI中显示着色地图的良好载体，然而它的缺陷也不少。比方地图大小无法随着外部切片的变化而**自适应**，《[Power BI着色地图自适应画布大小](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247488505&idx=1&sn=6cac4f79e237a5dff6bd9aca60c2b9b9&chksm=97db2aa9a0aca3bf14104666ebf89cd4f18964e67a929b3ae75d159ef0746aeed6e36c718139&scene=21#wechat_redirect)》给出了一种解决思路。

地图不仅仅可以填充颜色，也可以条件格式变换边框颜色《[Power BI 地图轮廓颜色变化](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247490967&idx=1&sn=0ffd9e0e94281c15b956bfe152f73b49&chksm=97db24c7a0acadd107768558de2112230330a3d5a31fdaf84a92b5eec2d06966c1dc91e3dee1&scene=21#wechat_redirect)》给出了办法。

**5. 地图高级应用**  

___

地图上能不能**叠加图表**，《[Power BI基于门店位置的业绩达成表现](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247489970&idx=1&sn=3dfb0a51718c02555e1b91369f39c633&chksm=97db20e2a0aca9f4266ed81e00ce099df4ea34a33462637668d2124276a15ef4db140330a444&scene=21#wechat_redirect)》讲解了叠加条形图的办法，其它图表类似。  

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/JHQQIBqYy6RjCQeH79rq9lOicFzxrhNwiaYHZwp85JkicicpPmoF7mYdJkYib6OVEg5EyOjNTtH7Eb5nboZSpkpBcibw/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

《[Power BI x EasyShu：Top商品门店分布地图可视化](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247489850&idx=1&sn=25692926aa2f778f20ad1b2da946a58f&chksm=97db206aa0aca97ce1b2856cb8f6bda866b695caf7b589863c5a36d13825336f3d9785950e2f&scene=21#wechat_redirect)》是另外一个地图叠加信息案例。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/JHQQIBqYy6R0zjN9IcXaQG2B1q6PiauhBhuBPrJn3VLhglvujibgJtCugOh7M71AwDX1zUXmicv3YTNgVXcx841QA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如何让地图滚动起来《[Power BI滚屏实战：多地图滚动轮播](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247490689&idx=1&sn=baeac1cca8aa6883bfd70d9e0cb87136&chksm=97db25d1a0acacc721f5198a80efb0bce0306f9c2c5a808dac8814e408ef2dc5d8ade20fe02a&scene=21#wechat_redirect)》讲解的很清楚。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/JHQQIBqYy6SU6bB5BMrVw7CDxgkglu8saZJM1xkMHibTJVicnVIvbKbvUibvGTIRwtuL5532AXXSQv0uKbvzWsLBQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

如何展示两个位置之间的流向关系《[视频课程：Power BI DAX自定义流向地图](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491232&idx=1&sn=43f6775b697cc4221670fe43b78dc5c5&chksm=97db27f0a0acaee69bb337daa6444955cd546ca578a346a5f7d37b944a115b77b5653e2547de&scene=21#wechat_redirect)》进行了细致的说明。  

![图片](https://mmbiz.qpic.cn/mmbiz_gif/JHQQIBqYy6SM9L2CvNiaaU6KKaQg4vynRTyNcCqhQCibibZUp4nKbWSa2WfaXicB2iaic8hgl3g0gfmG6DT07FPibILsQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

以上。读者如遇到SVG着色地图的使用问题，欢迎留言。  

___

星球将在2023年1月1日涨价，有兴趣的读者不要错过。详细介绍：[Power BI业务实战及图表开发社群&视频课程](http://mp.weixin.qq.com/s?__biz=MzIxOTQ5MjQxNQ==&mid=2247491267&idx=1&sn=9f8011a4c2a7f38f17b6ef4168625c63&chksm=97db2793a0acae853c07277e58d55c0b8db67e953b44228508b7282f4e907af330cf64efbf51&scene=21#wechat_redirect)
