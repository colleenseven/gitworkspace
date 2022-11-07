---
create_date: 2022-10-31 12:45
tags:
  - whole/汇总
status: 状态为空
uid: null
date updated: 2022-11-06 20:52
---

只看有一定价值的商业洞察，阅读量>=1w

阅读进度：2022年11月05日

#### 总计

```dataview
table status,category,create_date,tags,author
from "Knowledge/商业洞察/刘润"
sort create_date DESC
```

#### 2022年11月文章

```dataview
table status,category,create_date,tags 
from "Knowledge/商业洞察/刘润"
where contains(create_date, "2022-11")
sort create_date DESC
```

#### 2022年10月文章

```dataview
table status,category,create_date,tags 
from "Knowledge/商业洞察/刘润"
where contains(create_date, "2022-10")
sort create_date DESC 
```
