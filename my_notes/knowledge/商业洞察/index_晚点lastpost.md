---
create_date: 2022-11-02 16:23
tags: null
status: 状态为空 
uid: 
---

关注社区团购，美团，美团优选，美团快驴，美团买菜，多多买菜，橙心优选，京喜拼拼，每日优鲜，叮咚买菜，同城生活，十荟团

阅读进度：2022年11月05日

#### 未阅读

```dataview
table status,category,create_date,tags,notes
from "Knowledge/商业洞察/晚点lastpost"
where status ="未阅读"
sort create_date DESC
```
#### 已完成

```dataview
table status,category,create_date,tags,notes,down
from "Knowledge/商业洞察/晚点lastpost"
where status ="已完成"
sort create_date DESC
```

