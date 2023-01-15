---
create_date: 2023-01-11 00:02
tags: null
status: 未阅读 
aliases: null
notes: False
ZK: 
category: 
uid: 
---

powerbi战友联盟文章统计：共有文章数`$= dv.pages('"PowerBI/PowerBI战友联盟"').length`条

### 2022文章汇总

```dataview
table status,category,create_date,tags,ZK,DAX,notes
from "PowerBI/PowerBI战友联盟"
where contains(create_date, "2022-")
sort create_date DESC 
```


### 2021文章汇总

