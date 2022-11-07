---
create_date: 2022-10-23 12:03
tags: whole/汇总
status: 状态为空 
uid: 
---


### 语言表达 

status: 已完成

```dataview
table create_date, status  
from "Web/知乎/语言表达"
where status = "已完成"
sort file.ctime asc
```

#### 文化写作

```dataview
list
from "知乎/文化写作"
sort file.ctime asc
```

