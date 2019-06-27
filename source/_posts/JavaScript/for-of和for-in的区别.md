---
title: for...of和for...in的区别
date: 2019-06-27 10:29:19
tags: JavaScript
categories: JavaScript
---
1. for...in 语句以原始插入顺序迭代对象的可枚举属性，还会遍历到继承的属性。
2. for...of 语句遍历可迭代对象定义要迭代的数据，仅会遍历自有属性。
<!-- more -->
```js
Object.prototype.objCustom = function() {}; 
Array.prototype.arrCustom = function() {};

let iterable = [3, 5, 7];
iterable.foo = 'hello';

for (let i in iterable) {
  console.log(i); // logs 0, 1, 2, "foo", "arrCustom", "objCustom"
}

for (let i in iterable) {
  if (iterable.hasOwnProperty(i)) {
    console.log(i); // logs 0, 1, 2, "foo"
  }
}

for (let i of iterable) {
  console.log(i); // logs 3, 5, 7
}
```