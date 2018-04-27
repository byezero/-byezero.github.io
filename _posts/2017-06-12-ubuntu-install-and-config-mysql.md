---
layout: post
title:  ubuntu下安装配置mysql
categories: JavaScript
tags:  mysql ubuntu
author: lassove
---

* content
{:toc}
    
## 安装mysql
终端输入:
```bash
apt-get install mysql-server
```
目前默认安装5.7,可按需指定版本.

## 配置

### 让外网可以访问

```bash
vim /etc/mysql/mysql.conf.d/mysqld.cnf  
```
在该文件里 注释调 bind-address = 127.0.0.1

### 新建用户

```bash
mysql> create user kang identified by '******';
Query OK, 0 rows affected (0.00 sec)

mysql> create database tree;
Query OK, 1 row affected (0.00 sec)

mysql> grant all on tree.* to 'kang'@'%';
Query OK, 0 rows affected (0.00 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)


```

### 修改用户host

