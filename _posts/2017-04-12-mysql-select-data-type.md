---
layout: post
title:  MYSQL数据库按字段类型查询表
categories: Mysql
tags:  mysql sql
author: lassove
---

* content
{:toc}

今天发现数据库的一些字段使用了`double`类型,导致了数据精度问题,为此决定将所有的`double`改为`DECIMAL`类型.一个个表去查看字段是否double比较繁琐,所以写了一个sql可以查询出指定数据库含有`double`类型的字段的表有哪些,记录一下:
```sql
select DISTINCT TABLE_NAME
from information_schema.columns
where table_schema = 'db.name' and data_type = 'double'
```
db.name需要替换为你要查询的数据库名称.