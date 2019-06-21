---
title: node服务编写
date: 2019-06-18 11:22:35
tags: -node -express
---
## 以下内容不分先后 仅为笔记
### node发送请求

```
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