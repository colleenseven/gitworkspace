---
notes: False
create_date: 2022-10-27 17:45
tags:
  - pbi
status: 状态为空
uid: null
date updated: 2022-11-20 20:57
---


## 函数抽取

Filter

```dataview
table status,category,create_date,tags,DAX,file.folder
from "PowerBI"
where contains(DAX, "FILTER")
sort create_date desc
```

## PowerBI战友联盟

powerbi战友联盟文章统计：共有文章数`$= dv.pages('"PowerBI/PowerBI战友联盟"').length`条

### 2022文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBI战友联盟"
where contains(create_date, "2022-")
sort create_date DESC 
```


### 2021文章汇总


## Powerbi星球

powerbi 星球文章统计：共有文章数`$= dv.pages('"PowerBI/PowerBi星球"').length`条



### 2022文章汇总

#### 202201文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-01")
sort create_date DESC 
```

#### 202202文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-02")
sort create_date DESC 
```

#### 202203文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-03")
sort create_date DESC 
```

#### 202204文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-04")
sort create_date DESC 
```

#### 202205文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-05")
sort create_date DESC 
```

#### 202206文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-06")
sort create_date DESC 
```

#### 202207文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-07")
sort create_date DESC 
```

#### 202208文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-08")
sort create_date DESC 
```

#### 202209文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-09")
sort create_date DESC 
```

#### 202210文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-10")
sort create_date DESC 
```
#### 202211文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-11")
sort create_date DESC 
```
#### 202212文章汇总 

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2022-12")
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
from "PowerBI/PowerBi星球"
where contains(create_date, "2021-07")
sort create_date DESC 
```

#### 202108文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2021-08")
sort create_date DESC 
```

#### 202109文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2021-09")
sort create_date DESC 
```

#### 202110文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2021-10")
sort create_date DESC 
```

#### 202111文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2021-11")
sort create_date DESC 
```

#### 202112文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBi星球"
where contains(create_date, "2021-12")
sort create_date DESC 
```
