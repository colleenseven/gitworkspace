---
create_date: 2021-01-17T20:21:32 (UTC +08:00)
tags:
aliases:
pagetitle: 如何为Power BI页面批量插入背景图片？
source: https://mp.weixin.qq.com/s/qcIeNTgA2Ae1hygs6cUYVg
author: 采悟
status: 未阅读
category:
notes: false
ZK: Origin
uid:
---

周末分享一个PowerBI页面设计小技巧。

PowerBI的页面背景可以插入图片，不过只能一页一页的添加，如果报表的页面很多，这样添加起来也会比较麻烦，能不能一次性为所有的页面批量添加背景图片呢？

通过页面设置无法做到批量添加，不过利用PowerBI的主题设置，通过修改主题代码的方式可以实现。

关于主题的设置以前也介绍过，比如：

[如何在Power BI中随心所欲的搭配色彩？](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484068978&idx=1&sn=33c435da5b89e10b7ba3a2a908746aec&chksm=8e0c48a5b97bc1b3d5be5769b95d148813985a7c13ab3f3f5b294abc4e8a5829dec2719deb90&scene=21#wechat_redirect)  

[Power BI切片器搜索框背景色缺陷的解决方案](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484071291&idx=1&sn=b65803396a44d2ea664b7e83adf96d58&chksm=8e0c41acb97bc8bae4bfa653771ff75bed793476befc641415ea0e173340552bca43a7bab83e&scene=21#wechat_redirect)  

几乎所有的格式设置都可以通过主题来调整，这里我们不涉及其他的主题代码，只看关于背景设置的代码，不过首先需要将图片转化为Base64代码。

Base64是一种基于64个可打印字符来表示二进制数据的方法，各种文件均可以转换为base64代码来表示，关于如何将图片转为base64代码，有很多在线转换工具可以使用，大家可以自行百度搜索，比如：http://www.fly63.com/tool/base64/ 

![图片](https://mmbiz.qpic.cn/mmbiz_png/aHEbZtANQJMFXwrYS6fE9fQ3ibNODZmK0oGmHOx7rkYZZic3c6UjSlGiaztOt4rKcGJAwFMqXhoIbibKaFRO18MXRw/640?wx_fmt=png&wxfrom=5&wx_lazy=1&wx_co=1)

假如我们想以这个图片作为页面背景：

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJMFXwrYS6fE9fQ3ibNODZmK0QdiaolH4My1WNbtjicY1jN60ibQ9icdnFOkAgMuTXgWc0v48GiauhNofTDQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

可以先将这个图片利用在线转换工具转换为base64代码，然后将base64粘贴到下面主题中的相应位置：

{"name":"PowerBI星球"

,"visualStyles": {

        "page": {

            "\*": {

                "background": \[

                    {

                        "image": {

                            "name": "image",

                            "scaling": "Fit",

                            "url": "**粘贴图片的base64代码**"

                        },

                        "transparency": 0

                    }

                \]

            }

        }

    }

}

主题的代码可以先在txt文本中编辑，保存后，再将后缀改为json即可生成一个主题。

将这个主题导入到PowerBI中，效果是这样的：

![图片](https://mmbiz.qpic.cn/mmbiz_gif/aHEbZtANQJMFXwrYS6fE9fQ3ibNODZmK0ic9jSNF4V8HoczaCZfVro1ibI9gv7osQnib9QDWxvYE0d3zEmIg8prkeQ/640?wx_fmt=gif&wxfrom=5&wx_lazy=1)

这样就可以一键更改所有页面的背景，并且，新建页面，自动也是这个图片的背景，是不是相当于PPT的母版呢？

当然，利用主题代码来设计依然太笨重，期待PowerBI能够真的像PPT一样，更方便无代码的更改报表的主题。

___

**PowerBI星球的**[**历史精华文章合辑**](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)**，值得你收藏学习：**  

[![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNn5eia186067w5or6WoVmwdm210CYQfaibhdzFvJvR59sFUgk13iauEzR4oLzGvXiaziaX8VJcB2sCbzg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)](http://mp.weixin.qq.com/s?__biz=MzA4MzQwMjY4MA==&mid=2484074255&idx=1&sn=0c183ee84fd7fcc4e9dfb6baf39580c0&chksm=8e0c5dd8b97bd4ce1a617be83fe88938a0ba49668102ca3d10794c0e530f38c2950df75cf2ee&scene=21#wechat_redirect)

___

如果你刚开始学习Power BI，可在微信公众号后台回复"PowerBI"，获取《七天入门PowerBI》电子书，轻松上手。

**成为PowerBI星球会员****，获取更多学习资源**

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/aHEbZtANQJNCQ4pzSiaQOMPia6kNbbF0gtVXYmWpicF9SVicdBBQYdaKG4icSfUTkS9dFIBW3NsL5ZrNpYH6icjgJaUA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)

↑ 扫码加入，和 2k+ 学习者一起成长
