---
aliases: null
notes: notes
create_date: 2022-10-28 23:40
tags: 汇总/全局
status: 状态为空
uid: 
---
#### 未完成歌曲汇总

```dataview
table status,create_date,singer,tags,notes
from "歌曲/原曲"
where status != "状态为空" and status != "已完成" 
sort create_date DESC 
```

#### 已完成歌曲

```dataview
table status,create_date,singer,tags, file.folder, notes
from "歌曲/原曲"
where status = "已完成"
sort create_date DESC 
```

#### 解析

```dataview
table status,create_date,tags, file.folder,notes
from "歌曲/解析"
sort create_date DESC 
```