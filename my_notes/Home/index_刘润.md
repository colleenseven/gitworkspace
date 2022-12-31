---
create_date: 2022-10-31 12:45
tags:
  - 汇总/全局
status: 状态为空
uid: null
date updated: 2022-11-06 20:52
---

只看有一定价值的商业洞察，阅读量>=1w

刘润共有微信文章数`$= dv.pages('"Interest/商业洞察/刘润"').length-dv.pages('"Interest/商业洞察/刘润/刘润notes"').length`条
共有笔记数：`$=dv.pages('"Interest/商业洞察/刘润/刘润notes"').length`条

同步进度：2022年11月20日
阅读进度：2022年11月20日

#### 2022年笔记文章

```dataview
table status,create_date,tags,notes,ZK,up
from "Interest/商业洞察/刘润/刘润notes"
sort create_date DESC
```

#### 2022年12月文章

```dataview
table status,category,create_date,tags,notes,ZK,down
from "Interest/商业洞察/刘润" and !"Interest/商业洞察/刘润/刘润notes"
where contains(create_date, "2022-12") 
sort create_date DESC 
```

#### 2022年11月文章

```dataview
table status,category,create_date,tags,notes,ZK,down
from "Interest/商业洞察/刘润" and !"Interest/商业洞察/刘润/刘润notes"
where contains(create_date, "2022-11") 
sort create_date DESC 
```

#### 2022年10月文章

```dataview
table status,category,create_date,tags,notes,ZK,down
from "Interest/商业洞察/刘润" and !"Knowledge/商业洞察/刘润/刘润notes"
where contains(create_date, "2022-10") 
sort create_date DESC 
```
