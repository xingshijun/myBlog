---
title: lnmp环境安装
date: 2019-06-25 11:22:35
tags: -MySQL
categories: MySQL
---

### 安装lnmp
    ```
    wget http://soft.vpser.net/lnmp/lnmp1.6.tar.gz -cO lnmp1.6.tar.gz && tar zxf lnmp1.6.tar.gz && cd lnmp1.6 && ./install.sh lnmp
    ```
    
    
### 安装FTP
    ```
    cd lnmp1.6  //其他版本的话自行更改和确定目录位置
    执行  ./pureftpd.sh 
    ``` 
    `lnmp ftp add` 添加ftp账号 
    设置ftp访问目录 一般是 `/home/wwwroot`