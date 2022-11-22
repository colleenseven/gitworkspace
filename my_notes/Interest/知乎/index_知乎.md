---
create_date: 2022-10-23 12:03
tags: zh 
status: 状态为空 
uid: 
---


### 人生感悟

#### 未完成 

```dataview
table create_date, status,tags  
from "Knowledge/知乎/人生感悟"
where status = !"已完成"
sort file.ctime asc
```

#### 已完成

```dataview
table create_date, status,tags  
from "Knowledge/知乎/人生感悟"
where status = "已完成"
sort file.ctime asc
```

### 文化写作

```dataview
list
from "知乎/文化写作"
sort file.ctime asc
```

