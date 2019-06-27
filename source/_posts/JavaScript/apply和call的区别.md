---
title: apply和call的区别
date: 2019-06-26 17:01:15
tags: JavaScript
categories: JavaScript
---
### apply
apply() 方法调用一个具有给定this值的函数，以及作为一个数组（或类似数组对象）提供的参数。  
<!-- more -->
```js
var numbers = [5, 6, 2, 3, 7];
var max = Math.max.apply(null, numbers);
console.log(max);// expected output: 7
```
### call
call() 方法使用一个指定的 this 值和单独给出的一个或多个参数来调用一个函数。  
```js
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

console.log(new Food('cheese', 5).name);// expected output: "cheese"
```