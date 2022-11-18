---
aliases: null
create_date: 2022-10-28 12:14
tags: null
status: 状态为空 
uid: 
---

### 启明星辰面试知识补充

```dataview
table create_date,status,tags,file.folder,notes 
from #qz/启明星辰 
where status= "已完成"
sort create_date DESC 
```

#### 已完成
```dataview
table create_date,status,tags,file.folder,notes 
from "求职面试"
where status= "已完成"
sort create_date DESC 
```

#### 未完成 

```dataview
table create_date,status,tags,file.folder,notes 
from "求职面试"
where status= "未阅读"
sort create_date DESC 
```



