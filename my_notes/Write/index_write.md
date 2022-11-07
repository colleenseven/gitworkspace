---
create_date: 2022-11-06 21:18
tags: whole/汇总
status: 状态为空
notes: False
uid: 
---

#### 未完成


#### 已发布

```dataview
table create_date, status, file.folder,tags  
from "Write/知乎"
where status = "已发布"
sort file.ctime asc
```
