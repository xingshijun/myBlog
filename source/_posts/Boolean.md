---
title: Boolean
date: 2019-06-26 11:40:12
tags: -JavaScript
---
### new Boolean([value])
```js
new Boolean(0);//Boolean {false}
new Boolean(-0);//Boolean {false}
new Boolean(null);//Boolean {false}
new Boolean(false);//Boolean {false}
new Boolean(NaN);//Boolean {false}
new Boolean(undefined);//Boolean {false}
new Boolean("");//Boolean {false}
new Boolean(document.all);//Boolean {false}
```
*当 Boolean 对象用于条件语句的时候（译注：意为直接应用于条件语句），任何不是 undefined 和 null 的对象，包括值为 false 的 Boolean 对象，都会被当做 true 来对待*
```js
var x = new Boolean(false);
if (x) {//!x 为false而不是true 即if(x)  =>  Boolean(x) =>  Boolean(new Boolean(false)) => true
  // 这里的代码会被执行
}

var x = false;//x 非Boolean 对象
if (x) {
  // 这里的代码不会执行
}
```
对于任何对象，即使是值为 false 的 Boolean 对象，当将其传给 Boolean 函数时，生成的 Boolean 对象的值都是 true
```js
var myFalse = new Boolean(false);   // false
var g = new Boolean(myFalse);       // true
var myString = new String("Hello");
var s = new Boolean(myString);      // true
```
