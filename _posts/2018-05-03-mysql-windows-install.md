---
layout: post
title:  "Mysql8.0 windows 压缩版安装"
categories: mysql
tags:  mysql 基础教程
author: byezero
---


{:TOC}

# Mysql8.0 windows 压缩版安装

## 下载压缩包

请点击 [官网下载地址](https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-8.0.11-winx64.zip) 进行下载

## 解压

个人建议解压到任意盘的根目录:

![](https://s1.ax1x.com/2018/05/03/CYOGb6.png)

## 创建配置文件

进入解压后的mysql目录,创建文件 `my.ini`  内容如下:

```ini
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8mb4 
[mysqld]
#设置3306端口
port = 3306 

# 设置mysql的安装目录(一定要与你自己的目录一致)
basedir=D:\\mysql-8.0.11-winx64
# 设置mysql数据库的数据的存放目录(一定要与你自己的目录一致)
datadir=D:\\mysql-8.0.11-winx64\\data

# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为UTF8
character-set-server=utf8mb4
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

## 安装与启动


1. 配置环境变量(以windows10 为例)
  -  按下`windows + i`键打开系统设置.
  -  在搜索框输入`查看高级系统设置`并回车.
  -  在弹出的`高级系统设置`窗口点击右下的`环境变量`.
  -  在弹出的窗口中选择`系统变量`里的`Path`变量值,并点击编辑.

![CYX1Jg.png](https://s1.ax1x.com/2018/05/03/CYX1Jg.png)
  -  继续在弹出的窗口中选择`新建`,然后在提示输入的位置输入你的mysql目录下的bin文件夹的路径.此处我们输入`D:\mysql-8.0.11-winx64\bin`


![CYXsSJ.png](https://s1.ax1x.com/2018/05/03/CYXsSJ.png)

  -  点击`确定`逐层关闭弹出的窗口.



  ​

2. 以管理员方式运行`cmd`
3. 输入`mysqld –initialize –user=mysql –console`回车,会在控制台显示初始密码,记录下来.
4. 输入`mysqld install` 回车 安装windows服务启动项.
   - 会在windows服务中增加mysql服务,并为自动启动,意味着以后开机就会自动启动mysql
5. 输入`net start mysql` 回车启动服务.

## 修改root密码

启动mysql服务后

继续在`cmd`输入

1. 输入`mysql -u root -p` 回车.

2. 提示你输入密码,请输入上面步骤你记录下来的初始密码并回车.

3. 你会进入到mysql的命令窗口.

4. 进行修改密码:

   ```sql
   use mysql；
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的密码';  
   FLUSH PRIVILEGES;   
   ```

   ​

   - 上述命令的`你的密码` 应根据自己的选择修改.
   - 注意,root用户有着最高的权限,如果你的数据库可供多人访问,建议root密码设置复杂点.