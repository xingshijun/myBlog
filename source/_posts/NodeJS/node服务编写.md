---
title: node服务编写
date: 2019-06-18 11:22:35
tags: node express
categories: Node
---
### node发送请求
<!-- more -->
```js
var request = require('request');
getData('https://www.baidu.com', {
		a: '1',
		b: '2'
	}).then((data) => {
		res.send(data);
	})
const getData = (url, param) => {
	return new Promise((resolve, reject) => {
		request.post({
			url: url,
			form: param
		}, function (error, response, data) {
			//如果请求成功则打印数据 否则显示错误信息
			if (!error && response.statusCode == 200) {
				console.log(data);
				resolve(data)
			} else {
				console.log(error);
				console.log(response.statusCode);
			}
		});
	})
}
```
### node定时任务

1. 安装node-schedule

   `yarn add node-schedule`

2. ```js
   var schedule = require('node-schedule');
   function scheduleCronstyle(){//定时任务 每分钟的第30秒执行
   	schedule.scheduleJob('30 * * * * *',function(){
   	console.log('scheduleCronstyle:'+new Date());
   	});
   }
   scheduleCronstyle();//开启定时器
   ```

3. 通配符意义  *  *  *  *  *  *

   6个占位符从左到右分别代表：秒、分、时、日、月、周几

   每分钟的第30秒触发： '30 * * * * *'

   每小时的1分30秒触发 ：'30 1 * * * *'

   每天的凌晨1点1分30秒触发 ：'30 1 1 * * *'

   每月的1日1点1分30秒触发 ：'30 1 1 1 * *'

   2019年的1月1日1点1分30秒触发 ：'30 1 1 1 2019*'

   每周1的1点1分30秒触发 ：'30 1 1 * * 1'
   
### linux后台运行node服务
    ```
    npm install -g pm2
    pm2 start app.js -i max //启动一个使用所有CPU核心的集群 app.js是启动服务的js
    pm2 list  //列出所有pm2开启的进程
    pm2 monit //查看运行状态
    pm2 logs //打印日志
    ```