---
aliases: null
create_date: 2022-10-28 12:14
tags: null
status: 状态为空 
uid: 
---

### 求职列表

| 日期           | 公司                         | 岗位                   | 状态 |  原因   | 
| -------------- | ---------------------------- | ---------------------- | ---- | --- |
| 2022年11月19日 | 华谊启明东方城市文化产业集群 | 运营及商业中心执行专员 |  拒绝面试    |   小破公司，注册资本100万，多年公众号不更新，官网全是吹  |
|                |                              |                        |      |     |



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



