---
title: MySQL安装使用.md
date: 2019-06-18 11:22:35
tags: -MySQL
---
### 1.下载MySQL
<https://dev.mysql.com/downloads/mysql/>

### 2.配置环境变量
变量名：`MYSQL_HOME`  
变量值：`C:\Program Files (x86)\mysql-8.0.16-winx64` 你的安装路径  
path里添加：`%MYSQL_HOME%\bin;`

### 3.生成data文件
以管理员身份运行cmd  
进入`C:\Program Files (x86)\mysql-8.0.16-winx64\bin`下  
执行命令：`mysqld --initialize-insecure --user=mysql`  在C:\Program Files (x86)\mysql-8.0.16-winx64目录下生成data目录  

### 4.启动服务
执行命令：`net start mysql`  启动mysql服务  
1.启动服务失败、服务名无效解决方法：  
执行命令：`mysqld -install`  即可（不需要my.ini配置文件）  
2.服务正在启动或停止中解决方法：  
需要去任务管理器中把mysql相关进程结束掉，重新启动即可  

### 5.登录mysql
登录mysql:(因为之前没设置密码，所以密码为空，不用输入密码，直接回车即可）  
`C:\Program Files (x86)\mysql-8.0.16-winx64\bin>mysql -u root -p`  
`Enter password: ******`  

### 6.查询用户密码
`mysql> select host,user,authentication_string from mysql.user;`

### 7.设置（或修改）root用户密码
设置（或修改）root用户密码：  
set password for root@localhost = password('123456')
`mysql> ALTER user 'root'@'localhost' IDENTIFIED BY '123456';` 设置密码为123456  
`mysql> flush privileges;` 相当于保存，执行此命令后，设置才生效，若不执行，还是之前的密码不变  

### 8.添加用户
```
mysql> create user 'time'@'localhost' identified by '123456';
// time 用户名
// localhost 只能本地访问，写为%代表所有外网IP都可以访问
// 123456 为用户密码
然后需要刷新授权
mysql> flush privileges;
```
### 9.删除用户
```
mysql> delete from mysql.user where user='time' and host='localhost';
// 然后需要刷新授权 否则下次添加用户时会报错
mysql> flush privileges;
```
### 10.修改远程连接授权:
```
mysql> update user set host='%' where user='root'; // %代表所有外网IP都可以访问
// 然后需要刷新授权 
mysql> flush privileges;
```

### 11.退出mysql
`mysql> quit`  
