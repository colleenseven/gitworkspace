---
create_date: 2021-09-09T22:42:49 (UTC +08:00)
tags: 
aliases: null
pagetitle: PowerQuery批量合并Excel，原来这个方法更好用
source: https://mp.weixin.qq.com/s/5GKaEt9vscgvI7E2hrttog
author: 采悟
status: 未阅读
category: 
notes: False
ZK: Origin
uid: 
---

之前分享过多次关于批量合并Excel的方法和技巧，如果你还不熟悉怎么做，可以参考这些文章：

[PowerQuery合并Excel的这些技巧你应该掌握](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484070803&idx=1&sn=826d571e4133872ff3bedb4ad4d524f9&chksm=8e0c4344b97bca5281787e9a0cf1a3f2571227316537b1ba7069c5bf5f600d4a4249cfc18932&scene=21#wechat_redirect)  

[PowerQuery批量合并多个Excel的指定列](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073950&idx=1&sn=022f2b8806518ff03648eeea76950223&chksm=8e0c5f09b97bd61f3dc5a7509181aa42fd3545d009b9b8715b0ef387d4f50dffe0833dfa8ce4&scene=21#wechat_redirect)  

[Power Query批量合并Excel，数据不是从第一行开始怎么办？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484073974&idx=1&sn=f1c63db1ed01cbabd2a3293d663205a4&chksm=8e0c5f21b97bd637760e8cd51c9888c667e3b586da5bad7581c1749c73802656b60cf16456c6&scene=21#wechat_redirect)

这些技巧可以应对绝大多数情况，但仍有例外的情况，这篇文章分享一个更灵活、更普适的方法，利用自定义函数批量合并Excel。

以前分享的思路是，先批量合并文件夹里面的所有的Excel表格，汇总完成后后再进行整理。

而利用自定义函数的思路是，**先对文件夹中的一个文件进行整理，并将处理的步骤封装成自定义函数，然后对文件夹中的所有文件调用该函数，最终实现所有文件的合并整理。**  

如果还不是太理解，这里用一个示例带你看看，这种方式是怎么实现文件的批量整理，然后合并到一起的。  

以这个文件夹为例，有2019年到2021年3个年度的Excel文件：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb09NaRbqzXpe9SDa9ex1NQBTmDfL9NVXzjyNiaiaSsI4jEcAgcuD4ic61HQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

而每年的数据结构分别是下面这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0zoqV2A0zApf6w5oOnZDxOfjOsG6mnt7kfP1Hx7QmU3YXia2NZGISN1g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb046L0MFLe2lyoY6KbxQ22T6fQibyoiaQsHCgd8T2icJ9E7Cc5WMAl6XNDQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0JNiaTGWV9iaA8Q9IpEb4Wp5Vv4xsnCQiaQy3fhgekuAjMibia7Pw8yiaXyXQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

看起来表的结构好像是相同的，但仔细观察这三个表，你会发现，**每个表的列名都是该年的月份，如果简单合并，就丢失了年月维度的信息，并且2021年的列数与其他两年还是不等的**，这都导致了不能按照之前的方法简单合并。  

由于上面几个表都是二维表，最后肯定要转换为一维表使用，那么，我们可以换个思路，先将每个表转换为一维表，一维表格式是完全相同的，最后再合并即可。  

当然不需要手工单独对每个表转换为一维表，只需转换一个，然后将这个表的转换步骤应用到文件夹中的每个表上即可，下面是操作步骤。

**1、将一个表导入到PowerQuery，并进行数据整理。**

比如先将2019年的表，导入并逆透视为一维表，处理后的效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0t96AIkNbI1ib34iczghWafykAA6pkWPfZibdwcIUddh1gI0bqq0yL6V6Q/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

如果对PowerQuery操作不了解，可以先看看这篇文章：[数据清洗中最常使用的十三招](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067158&idx=1&sn=4ad955112df2f40a93b684ed9147f26e&chksm=8e0c7181b97bf89777ae3d9de929867745edcbbfe1f2b396761c0cec716b86ee31e439279add&scene=21#wechat_redirect)

[](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484067158&idx=1&sn=4ad955112df2f40a93b684ed9147f26e&chksm=8e0c7181b97bf89777ae3d9de929867745edcbbfe1f2b396761c0cec716b86ee31e439279add&scene=21#wechat_redirect)

**2、将第一步的查询封装成自定义函数。**

右键该查询，创建函数，可以命名为"单文件处理"。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0GBHoLJrvEbNc7Z0e02vU6bZz20nAvYGkDzcfmYkk11FA4vwgs9ibdGA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

生成自定义函数后，在编辑器中修改M代码，将excel文件的路径更改为自定义函数的参数：

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0N97H3T8oRIUFMJHu5czo62NRAuI34rULPyY2vT5oA08vpcHiaLOmRcQ/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后我们只要将每个文件的路径找到，作为这个自定义函数的参数就可以了。  

**3、PowerQuery导入文件夹，获取每个文件的路径。**

文件夹导入后，选中Name和FolderPath列，删除其他列，只保留这两列：  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0o1yePiaAzBXK48ywxGNaC1XaZR14pT0QFicEYjJdmeenN14knQv9kXDA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后将这两列合并，就得到了每个文件的完整路径。

**4、调用自定义函数，合并完成。**

在第三步的基础上，调用第2步建好的自定义函数，将每个文件的完整路径作为参数。  

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0ibV3UOK8l9AoHSVBoFP8ZFsSPkapJYf0dkJVKvQ9aExA17iaHzadIzSA/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

然后展开数据，就直接得到了3个文件汇总并整理好的一维表。

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJPibRkQTpkk3Ropx14aIkWb0YnZfNWrpxcqx1ibh6FVRfQO4QrUGscnsAvI8lvoTOofgFthJStxRia7g/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

以上就是利用自定义函数批量汇总的全部步骤，是不是也挺简单。  

这种方法的优点如下：

-   **更加灵活**：对于不能直接简单的合并的（如本文示例），也可以处理；
    
-   **速度更快**：先对一个文件进行整理，然后再汇总，相比先汇总再整理，更节省时间，对于文件多、数据量大、以及需要较为复杂处理的合并尤为如此。
    

本文的练习数据，可以在「PowerBI星球」公众号对话框发送关键字“**自定义函数**批******量合并**”下载。

___

**[PowerBI商业数据分析](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074987&idx=1&sn=5cf4ba4b683ee9136bb7a26f6e9bcf01&chksm=8e0c533cb97bda2add48a4576b9c1e230249a5a4160dd93cd677a37ea21d26fc9cc26fc4cb1c&scene=21#wechat_redirect)**

帮你从0到1，轻松上手PowerBI

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJNuVIqc0mzbKDNPmI0mwcTkvUibMVjf4z1bY0MYFh7lAkqrcHiaEHE4UicvjJjibpmkxJjc4TDlVO04qg/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

___

\-精彩推荐-

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJPUabZXugXKNdmeUzxwJM4OyUpTibBJjoq1jk8CzVZJz6s4nJRW1ViammT4ecqAJ7iapDccKNNrwtLYQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077212&idx=1&sn=bb3dac9becf80b5d929e5dc8405158dd&chksm=8e13a84bb964215d6362f78768cdefa18def4dfc8cd5c14f075442431604ed9c9729e4051a4b&scene=21#wechat_redirect)

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNNJia1fBccdeD4HTtvAuUibkNI6YYicVJ3RPhufJhoh3lzY1e1dgUyxy6yGkk4UvZcuTfVGTc89iaI3Q/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484077048&idx=1&sn=b3da0a4079ed8366c67982912e795d59&chksm=8e13ab2fb964223978c16d5647e4a28eaeb50bc7338c4e82f4e14f2cddc8bb844b956f09beb6&scene=21#wechat_redirect)

如果你刚开始学习Power BI，也可以在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松入门。

**成为PowerBI星球会员****，获取更多学习资源**

↑ 扫码加入，和 3k+ 学习者一起成长
