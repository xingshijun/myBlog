---
title: forEach和map
date: 2019-06-27 11:30:52
tags: JavaScript Array
categories: JavaScript
---
### forEach
`arr.forEach(callback[, thisArg]);//返回值：undefined` 

<!-- more -->

callback 
```
currentValue 数组中正在处理的当前元素
index 数组中正在处理的当前元素索引
array 正在操作的数组
```
thisArg 可选  
`当执行回调函数时用作 this 的值 `  
* 注意： 没有办法中止或者跳出 forEach() 循环，除了抛出一个异常。如果你需要这样，使用 forEach() 方法是错误的。

### map
`arr.map(callback[, thisArg]);//返回值：一个新数组，每个元素都是回调函数的结果`  
callback 
```
currentValue 数组中正在处理的当前元素
index 数组中正在处理的当前元素索引
array 正在操作的数组
```
thisArg 可选  
`当执行回调函数时用作 this 的值 `  
* map 不修改调用它的原数组本身
* 使用 map 方法处理数组时，数组元素的范围是在 callback 方法第一次调用之前就已经确定了。在 map 方法执行的过程中：原数组中新增加的元素将不会被 callback 访问到；若已经存在的元素被改变或删除了，则它们的传递到 callback 的值是 map 方法遍历到它们的那一时刻的值；而被删除的元素将不会被访问到。

### forEach和map的区别
1. 返回值不同
    * forEach 返回undefined  
    * map 返回一个新数组，每个元素都是回调函数的结果  
2. 修改原数组
    * forEach 会改变原数组的数据
    * map 会创建一个新数组不会改变原数组的数据