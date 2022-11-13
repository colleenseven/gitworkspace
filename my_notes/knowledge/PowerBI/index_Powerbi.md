---
create_date: 2022-10-27 17:45 
tags: whole/汇总
status: 状态为空
uid: 
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

## 函数抽取

```dataview
table status,category,create_date,tags,file.folder
from "Knowledge/PowerBI"
where contains(DAX, "UNION")
```

## PowerBI战友联盟

### 2022文章汇总

### 2021文章汇总

## PowerBI白茶

### 2022文章汇总

### 2021文章汇总
 
## Powerbi星球

powerbi 星球文章统计：共有文章数`$= dv.pages('"Knowledge/PowerBI/Web_PowerBi星球"').length`条

### 2022文章汇总

#### 202201文章汇总

#### 202202文章汇总

#### 202203文章汇总

#### 202204文章汇总

#### 202205文章汇总

#### 202206文章汇总
```dataview
table status,category,create_date,tags,file.folder
from "Knowledge/PowerBI/Web_PowerBi星球"
where contains(create_date, "2022-06")
sort create_date DESC 
```

#### 202207文章汇总
```dataview
table status,category,create_date,tags,file.folder 
from "Knowledge/PowerBI/Web_PowerBi星球"
where contains(create_date, "2022-07")
sort create_date DESC 
```

#### 202208文章汇总
```dataview
table status,category,create_date,tags,file.folder
from "Knowledge/PowerBI/Web_PowerBi星球"
where contains(create_date, "2022-08")
sort create_date DESC 
```


#### 202209文章汇总

```dataview
table status,category,create_date,tags,file.folder
from "Knowledge/PowerBI/Web_PowerBi星球"
where contains(create_date, "2022-09")
sort create_date DESC 
```

#### 202210文章汇总
```dataview
table status,category,create_date,tags,file.folder
from "Knowledge/PowerBI/Web_PowerBi星球"
where contains(create_date, "2022-10")
sort create_date DESC 
```




### 2021文件汇总