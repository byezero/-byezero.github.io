---
layout: post
title:  "Mysql5.7 windows 压缩版安装"
categories: mysql
tags:  mysql 基础教程
author: byezero
---


{:TOC}

# Mysql5.7 windows 压缩版安装

## 下载压缩包

请点击 [官网下载地址](https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.22-winx64.zip) 进行下载

**注意**:mysql5.7版本需要`Microsoft Visual C++ 2013 Redistributable Package`支持.

[点此下载](https://www.microsoft.com/en-us/download/details.aspx?id=40784)

保险起见,64位系统建议下载并安装`vcredist_x86`和`vcredist_x64`

下载完成后安装即可.

## 解压

个人建议解压到任意盘的根目录:

## 安装与启动

1. 以管理员方式运行`cmd`
2. 输入`D:`切换盘符,输入`cd D:\mysql-5.7.22-winx64\bin`进入`bin`目录.
3. 输入`mysqld --initialize --user=mysql --console`回车,会在控制台显示初始密码,记录下来.
4. 创建文件 `my.ini`  内容如下:

	```ini
    [mysql]
    # 设置mysql客户端默认字符集
    default-character-set=utf8mb4 
    [mysqld]
    #设置3306端口
    port = 3306 

    # 设置mysql的安装目录(一定要与你自己的目录一致)
    basedir=D:\\mysql-5.7.22-winx64
    # 设置mysql数据库的数据的存放目录(一定要与你自己的目录一致)
    datadir=D:\\mysql-5.7.22-winx64\\data

    # 允许最大连接数
    max_connections=200
    # 服务端使用的字符集默认为UTF8
    character-set-server=utf8mb4
    # 创建新表时将使用的默认存储引擎
    default-storage-engine=INNODB
	```

5. 输入`mysqld install` 回车 安装windows服务启动项.
   - 会在windows服务中增加mysql服务,并为自动启动,意味着以后开机就会自动启动mysql
6. 输入`net start mysql` 回车启动服务.

## 修改root密码

启动mysql服务后

继续在`cmd`输入

1. 输入`mysql -u root -p` 回车.

2. 提示你输入密码,请输入上面步骤你记录下来的初始密码并回车.

3. 你会进入到mysql的命令窗口.

4. 进行修改密码:

   ```sql
   ALTER USER 'root'@'localhost' IDENTIFIED BY '你的密码';
   FLUSH PRIVILEGES;   
   ```
   - 上述命令的`你的密码` 应根据自己的选择修改.
   - 注意,root用户有着最高的权限,如果你的数据库可供多人访问,建议root密码设置复杂点.

## 新增数据库与用户

**注意**  以下操作均在mysql命令窗口下:

### 新增数据库

- 命令 `create database study;` 回车.
- 其中,`study`是要新增的数据库名.
- 注意`;`是sql语句/命令的结束符,不可省略.

### 使用新增的数据库

- 命令 `use study;` 回车.
- 其中,`study`是要使用的数据库名.

### 新增用户并授权

```sql
use mysql;
--创建yuanlei用户并设置密码为s1s2s3
create user 'yuanlei'@'localhost' identified by 's1s2s3';
--授权
GRANT ALL ON study.* TO `yuanlei`@`localhost`;
--刷新权限
FLUSH PRIVILEGES; 

```

**注意**上述用户只能本机访问数据库,若要局域网/外网访问,需将`'127.0.0.1'`替换为`'%'`

## 其它有用的命令

###  切换用户

- 输入`exit`退出当前用户,退回到`cmd`.
- 继续输入`mysql -u yuanlei -p`回车.
- 提示输入密码,输入上面设置的密码,本例为`s1s2s3`

### 显示所有数据库

`show databases;`

###  显示所有的表

`show tables;`



