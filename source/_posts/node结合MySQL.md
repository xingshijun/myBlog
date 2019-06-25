---
title: node结合MySQL
date: 2019-06-18 11:22:35
tags: -node -MySQL
categories: Node
---
### 使用node进行数据库操作
<!-- more -->
```
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : '123456',
  database : 'test'
});
/* MySql数据库连接参数说明：
参数                  描述
host                    主机地址 （默认：localhost）
user                    用户名
password                密码
port                    端口号 （默认：3306）
database                数据库名
charset                 连接字符集（默认：'UTF8_GENERAL_CI'，注意字符集的字母都要大写）
localAddress            此IP用于TCP连接（可选）
socketPath              连接到unix域路径，当使用 host 和 port 时会被忽略
timezone                时区（默认：'local'）
connectTimeout          连接超时（默认：不限制；单位：毫秒）
stringifyObjects        是否序列化对象
typeCast                是否将列值转化为本地JavaScript类型值 （默认：true）
queryFormat             自定义query语句格式化方法
supportBigNumbers       数据库支持bigint或decimal类型列时，需要设此option为true （默认：false）
bigNumberStrings        supportBigNumbers和bigNumberStrings启用 强制bigint或decimal列以JavaScript字符串类型返回（默认：false）
dateStrings             强制timestamp,datetime,data类型以字符串类型返回，而不是JavaScript Date类型（默认：false）
debug                   开启调试（默认：false）
multipleStatements      是否许一个query中有多个MySQL语句 （默认：false）
flags                   用于修改连接标志
ssl                     使用ssl参数（与crypto.createCredenitals参数格式一至）或一个包含ssl配置文件名称的字符串，目前只捆绑Amazon RDS的配置文件
 */

// 执行数据库连接 
connection.connect();

var sqlstring = "";
 
// 创建表
sqlstring = "Create Table MYTABLE (name VARCHAR(20), sex CHAR(1))"
connection.query(sqlstring, function (err, results, fields) {
    if (err) {
         console.log('[UPDATE ERROR] - ', err.message);
        return;
    }
    console.log('--------------------------CREATE----------------------------');       
    console.log('CREATE TABLE:', results);        
    console.log('------------------------------------------------------------\n\n');  
});

// 插入数据
sqlstring = "Insert into MYTABLE Values('Michael', 'm')";
connection.query(sqlstring, function (err, result) {
    if(err){
        console.log('[INSERT ERROR] - ', err.message);
        return;
    }        
 
   console.log('--------------------------INSERT----------------------------');       
   console.log('INSERT ID - ', result);        
   console.log('------------------------------------------------------------\n\n');  
});

// 更新数据
sqlstring = "Update MYTABLE Set name = 'Michael Jordan' Where sex = 'm'";
connection.query(sqlstring, function (err, result) {
    if(err){
        console.log('[UPDATE ERROR] - ', err.message);
        return;
    }        
    console.log('--------------------------UPDATE----------------------------');
    console.log('UPDATE affectedRows - ', result.affectedRows);
    console.log('------------------------------------------------------------\n\n');  
});

// 查询数据
sqlstring = "Select * From MYTABLE";
connection.query(sqlstring, function (err, result) {
    if(err){
        console.log('[SELECT ERROR] - ', err.message);
        return;
    }
 
    console.log('--------------------------SELECT---------------------------');
    console.log('SELECT - ', result);
    console.log('------------------------------------------------------------\n\n');   
});

//删除数据
sqlstring = "Delete From MYTABLE";
connection.query(sqlstring, function (err, result) {
    if(err){
        console.log('[DELETE ERROR] - ', err.message);
        return;
    }        
 
    console.log('--------------------------DELETE----------------------------');
    console.log('DELETE affectedRows - ', result.affectedRows);
    console.log('------------------------------------------------------------\n\n');  
});

//删除表格
sqlstring = "Drop Table MYTABLE";
connection.query(sqlstring, function (err, result) {
    if(err){
        console.log('[DROP ERROR] - ', err.message);
        return;
    }        
 
    console.log('--------------------------DROP-----------------------------');
    console.log('DROP TABLE :', result.affectedRows);
    console.log('------------------------------------------------------------\n\n');    
});


// 断开数据库连接
connection.end();
```