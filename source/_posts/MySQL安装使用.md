---
title: MySQL安装使用
date: 2019-06-18 11:22:35
tags: -MySQL
categories: MySQL
---
###下载MySQL
<https://dev.mysql.com/downloads/mysql/>

### 配置环境变量
变量名：`MYSQL_HOME`  
变量值：`C:\Program Files (x86)\mysql-8.0.16-winx64` 你的安装路径  
path里添加：`%MYSQL_HOME%\bin;`
<!-- more -->
### 生成data文件
以管理员身份运行cmd  
进入`C:\Program Files (x86)\mysql-8.0.16-winx64\bin`下  
执行命令：`mysqld --initialize-insecure --user=mysql`  在C:\Program Files (x86)\mysql-8.0.16-winx64目录下生成data目录  

### 启动服务
执行命令：`net start mysql`  启动mysql服务  
1.启动服务失败、服务名无效解决方法：  
执行命令：`mysqld -install`  即可（不需要my.ini配置文件）  
2.服务正在启动或停止中解决方法：  
需要去任务管理器中把mysql相关进程结束掉，重新启动即可  

### 登录mysql
登录mysql:(因为之前没设置密码，所以密码为空，不用输入密码，直接回车即可）  
`C:\Program Files (x86)\mysql-8.0.16-winx64\bin>mysql -u root -p`  
`Enter password: ******`  

### 查询用户密码
`mysql> select host,user,authentication_string from mysql.user;`

### 设置（或修改）root用户密码
设置（或修改）root用户密码：  
`mysql> ALTER user 'root'@'localhost' IDENTIFIED BY '123456';` 设置密码为123456  
`mysql> flush privileges;` 相当于保存，执行此命令后，设置才生效，若不执行，还是之前的密码不变  

### 添加用户
```
mysql> create user 'time'@'localhost' identified by '123456';
// time 用户名
// localhost 只能本地访问，写为%代表所有外网IP都可以访问
// 123456 为用户密码
然后需要刷新授权
mysql> flush privileges;
```
### 删除用户
```
mysql> delete from mysql.user where user='time' and host='localhost';
// 然后需要刷新授权 否则下次添加用户时会报错
mysql> flush privileges;
```
### 修改远程连接授权:
```
mysql> update user set host='%' where user='root'; // %代表所有外网IP都可以访问
// 然后需要刷新授权 
mysql> flush privileges;
```

### 退出mysql
`mysql> quit`  

### Mysql创建数据库字符集的选择

- 一般选择utf8.下面介绍一下utf8与utfmb4的区别

  utf8mb4兼容utf8，且比utf8能表示更多的字符

  unicode编码区从1 ～ 126就属于传统utf8区，utf8mb4也兼容这个区，126行以下就是utf8mb4扩充区

- 排序说明

  utf8_general_ci 不区分大小写，这个你在注册用户名和邮箱的时候就要使用。

  utf8_general_cs 区分大小写，如果用户名和邮箱用这个 就会造成不良后果

  utf8_bin:字符串每个字符串用二进制数据编译存储。 区分大小写，而且可以存二进制的内容

  utf8_unicode_ci和utf8_general_ci对中、英文来说没有实质的差别。

  utf8_general_ci校对速度快，但准确度稍差。（准确度够用，一般建库选择这个）

  utf8_unicode_ci准确度高，但校对速度稍慢

### MySQL支持的数据类型

1. **数值类型**

   | 整数类型     | 字节  | 范围（有符号）                                         | 范围（无符号）                 | 用途       |
   | ------------ | ----- | ------------------------------------------------------ | ------------------------------ | ---------- |
   | TINYINT      | 1字节 | (-128,127)                                             | (0,255)                        | 小整数值   |
   | SMALLINT     | 2字节 | (-32 768,32 767)                                       | (0,65 535)                     | 大整数值   |
   | MEDIUMINT    | 3字节 | (-8 388 608,8 388 607)                                 | (0,16 777 215)                 | 大整数值   |
   | INT或INTEGER | 4字节 | (-2 147 483 648,2 147 483 647)                         | (0,4 294 967 295)              | 大整数值   |
   | BIGINT       | 8字节 | (-9 233 372 036 854 775 808,9 223 372 036 854 775 807) | (0,18 446 744 073 709 551 615) | 极大整数值 |
   
   FLOAT(单精度浮点数值 4字节) (-3.402 823 466 E+38,1.175 494 351 E-38),0,(1.175 494 351 E-38,3.402 823 466 351 E+38) 0,(1.175 494 351 E-38,3.402 823 466 E+38)  
   
   DOUBLE ( 双精度浮点数值 8字节 )  (1.797 693 134 862 315 7 E+308,2.225 073 858 507 201 4 E-308),0,(2.225 073 858 507 201 4 E-308,1.797 693 134 862 315 7 E+308) 0,(2.225 073 858 507 201 4 E-308,1.797 693 134 862 315 7 E+308) 
   
   DECIMAL 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 依赖于M和D的值 依赖于M和D的值
   
2. **字符串类型**
   
    | 字符串类型 | 字节大小                    | 描述及存储需求               |
    | ---------- | --------------------------- | ---------------------------- |
    | CHAR       | 0-255字节                   | 定长字符串                   |
    | VARCHAR    | 0-255字节                   | 变长字符串                   |
    | TINYBLOB   | 0-255字节        不超过 255 | 个字符的二进制字符串         |
    | TINYTEXT   | 0-255字节                   | 短文本字符串                 |
    | BLOB       | 0-65535字节                 | 二进制形式的长文本数据       |
    | TEXT       | 0-65535字节                 | 长文本数据                   |
    | MEDIUMBLOB | 0-16 777 215字节            | 二进制形式的中等长度文本数据 |
    | MEDIUMTEXT | 0-16 777 215字节            | 中等长度文本数据             |
    | LOGNGBLOB  | 0-4 294 967 295字节         | 二进制形式的极大文本数据     |
    | LONGTEXT   | 0-4 294 967 295字节         | 极大文本数据                 |
    
    VARBINARY(M) 允许长度0-M个字节的定长字节符串，值的长度+1个字节
    
    BINARY(M) 允许长度0-M个字节的定长字节符串
    
3. **日期和时间类型**
    | 类型      | 大小(字节) | 范围                                    | 格式          用途                       |
    | --------- | ---------- | --------------------------------------- | ---------------------------------------- |
    | DATE      | 4          | 1000-01-01/9999-12-31                   | YYYY-MM-DD    日期值                     |
    | TIME      | 3          | '-838:59:59'/'838:59:59'                | HH:MM:SS    时间值或持续时间             |
    | YEAR      | 1          | 1901/2155                               | YYYY       年份值                        |
    | DATETIME  | 8          | 1000-01-01 00:00:00/9999-12-31 23:59:59 | YYYY-MM-DD HH:MM:SS 混合日期和时间值     |
    | TIMESTAMP | 4          | 1970-01-01 00:00:00/2037                | YYYYMMDD HHMMSS 混合日期和时间值，时间戳 |
    

### mySQL添加用户可访问数据库
    ```
    grant all privileges on database.* to username@'%' identified by 'password';
    flush privileges;
    ```