---
create_date: 2022-11-18 20:06
tags: null
status: 状态为空
aliases: 儿童经典国学读本唐诗
author: 杨平
notes: False
ISBN: 978-7-5110-3854-8
publisher: 海豚出版社
uid: 
---

### 已完成

```dataview
table create_date,author,status,tags,location
from "成长记录/小学语文/唐诗"
where status = "已完成"
sort location DESC 
```

### 未完成

```dataview
table create_date,author,status,tags,location
from "成长记录/小学语文/唐诗"
where status = !"已完成"
sort author DESC 
```

