---
notes: False
create_date: 2022-10-27 17:45
tags:
  - pbi
status: 状态为空
uid: null
date updated: 2022-11-20 20:57
---

### 概述

powerbi软件公众号情况说明

<mark style="background: #FF5582A6;">BI使徒</mark>：持续更新，雷元，专注于bi知识解析及资讯分享领域，阅读价值 3star。 
<mark style="background: #FF5582A6;">Excel商务智能PowerPivot</mark>：2019年后长期不更新，但是有几篇核心文章有价值，其他阅读价值 0star。 
<mark style="background: #FF5582A6;">Excel到PowerBI</mark>：持续更新，黄海剑，专注于办公软件使用技巧，阅读价值 4star
<mark style="background: #FF5582A6;">Excel催化剂</mark>：持续更新，但内容基本与Excel插件相关，阅读价值 0star
<mark style="background: #FF5582A6;">简快Excel之PowerBI建模分析</mark>：很少更新，内容价值不大，阅读价值 0star
<mark style="background: #FF5582A6;">PowerPivot工坊</mark>：早期内容干货，后续逐渐水化，入门pbi以后，不需要再仔细阅读，阅读价值 2star 
<mark style="background: #FF5582A6;">PowerBI极客</mark>：高飞，pbi数据分析和可视化，更新很少，阅读价值 1star
<mark style="background: #FF5582A6;">PowerBI老司机</mark>：pbi学习心得，多数是函数，学习价值不大，阅读价值 1star
<mark style="background: #FF5582A6;">PowerBI大师</mark>：马世权，PBI教程通俗易懂，但是更新较少，阅读价值 1star
<mark style="background: #FF5582A6;">悦策PowerBI</mark>：微软pbi官方平台，没有什么干货，阅读价值 0star
<mark style="background: #FF5582A6;">PowerBI白茶</mark>： 罗喆，专注研究pbi的函数，但是撰文风格一般，阅读价值3star

## 函数抽取

VALUES

```dataview
table status,category,create_date,tags,DAX,file.folder
from "Interest/PowerBI"
where contains(DAX, "VALUES")
```

## PowerBI战友联盟

powerbi战友联盟文章统计：共有文章数`$= dv.pages('"Interest/PowerBI/PowerBI战友联盟"').length`条

### 2022文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBI战友联盟"
where contains(create_date, "2022-")
sort create_date DESC 
```


### 2021文章汇总


## Powerbi星球

powerbi 星球文章统计：共有文章数`$= dv.pages('"Interest/PowerBI/PowerBi星球"').length`条

### 2022文章汇总

#### 202201文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-01")
sort create_date DESC 
```

#### 202202文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-02")
sort create_date DESC 
```

#### 202203文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-03")
sort create_date DESC 
```

#### 202204文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-04")
sort create_date DESC 
```

#### 202205文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-05")
sort create_date DESC 
```

#### 202206文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-06")
sort create_date DESC 
```

#### 202207文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-07")
sort create_date DESC 
```

#### 202208文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-08")
sort create_date DESC 
```

#### 202209文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-09")
sort create_date DESC 
```

#### 202210文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-10")
sort create_date DESC 
```
#### 202211文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2022-11")
sort create_date DESC 
```

### 2021文件汇总

#### 202101文章汇总

#### 202102文章汇总

#### 202103文章汇总

#### 202104文章汇总

#### 202105文章汇总

#### 202106文章汇总

#### 202107文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2021-07")
sort create_date DESC 
```

#### 202108文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2021-08")
sort create_date DESC 
```

#### 202109文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2021-09")
sort create_date DESC 
```

#### 202110文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2021-10")
sort create_date DESC 
```

#### 202111文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2021-11")
sort create_date DESC 
```

#### 202112文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "Interest/PowerBI/PowerBi星球"
where contains(create_date, "2021-12")
sort create_date DESC 
```
