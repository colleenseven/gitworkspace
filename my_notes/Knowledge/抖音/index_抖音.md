---
create_date: 2022-11-05 12:08
tags: null
status: 状态为空
uid: 
---
### 已完成

```dataview
table status,create_date,tags, file.folder
from "Knowledge/抖音"
where status = "已完成"
sort create_date DESC 
```

### 未阅读

```dataview
table status,create_date,tags, file.folder
from "Knowledge/抖音"
where status = "未阅读"
sort create_date DESC 
```