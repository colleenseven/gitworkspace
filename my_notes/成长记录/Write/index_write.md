---
aliases: null
create_date: 2022-11-06 21:18
tags: 汇总/全局
status: 状态为空
notes: False
uid: 
---

#### 未完成

```dataview
table create_date, status, file.folder,tags  
from "Write/知乎"
where status = "未阅读"
sort file.ctime asc
```

#### 已发布

```dataview
table create_date, status, file.folder,tags  
from "Write/知乎"
where status = "已发布"
sort file.ctime asc
```
