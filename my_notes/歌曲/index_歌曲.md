---
create_date: 2022-10-28 23:40
tags: null
status: 状态为空
uid: 
---
#### 未完成歌曲汇总
```dataview
table status,create_date,singer,tags 
from "歌曲"
where status != "状态为空" and status != "已完成" 
sort create_date DESC 
```

#### 已完成歌曲

```dataview
table status,create_date,singer,tags 
from "歌曲"
where status = "已完成"
sort create_date DESC 
```