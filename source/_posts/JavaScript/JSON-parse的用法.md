---
title: JSON.parse的用法
date: 2019-06-26 18:12:39
tags: JavaScript JSON
categories: JavaScript
---
### JSON.parse(text[, reviver])
text  
要被解析成JavaScript值的字符串，关于JSON的语法格式。
reviver 可选  
转换器, 如果传入该参数(函数)，可以用来修改解析生成的原始值，调用时机在parse函数返回之前
<!-- more -->
#### reviver用法
```js
JSON.parse('{"p": 5}', function (k, v) {
    if(k === '') return v;     // 如果到了最顶层，则直接返回属性值，
    return v * 2;              // 否则将属性值变为原来的 2 倍。
});                            // { p: 10 }

JSON.parse('{"one": 1, "two": 2,"three": {"four": 4, "five": {"six": 6}}}', function (k, v) {
    console.log(k); // 输出当前的属性名，从而得知遍历顺序是从内向外的，
                    // 最后一个属性名会是个空字符串。
    return v;       // 返回原始属性值，相当于没有传递 reviver 参数。
});

// one
// two
// four
// six
// five
// three 
// ""
```
### *IE7及以下使用JSON
```js
if (!window.JSON) {
  window.JSON = {
    parse: function(sJSON) { return eval('(' + sJSON + ')'); },
    stringify: (function () {
      var toString = Object.prototype.toString;
      var isArray = Array.isArray || function (a) { return toString.call(a) === '[object Array]'; };
      var escMap = {'"': '\\"', '\\': '\\\\', '\b': '\\b', '\f': '\\f', '\n': '\\n', '\r': '\\r', '\t': '\\t'};
      var escFunc = function (m) { return escMap[m] || '\\u' + (m.charCodeAt(0) + 0x10000).toString(16).substr(1); };
      var escRE = /[\\"\u0000-\u001F\u2028\u2029]/g;
      return function stringify(value) {
        if (value == null) {
          return 'null';
        } else if (typeof value === 'number') {
          return isFinite(value) ? value.toString() : 'null';
        } else if (typeof value === 'boolean') {
          return value.toString();
        } else if (typeof value === 'object') {
          if (typeof value.toJSON === 'function') {
            return stringify(value.toJSON());
          } else if (isArray(value)) {
            var res = '[';
            for (var i = 0; i < value.length; i++)
              res += (i ? ', ' : '') + stringify(value[i]);
            return res + ']';
          } else if (toString.call(value) === '[object Object]') {
            var tmp = [];
            for (var k in value) {
              if (value.hasOwnProperty(k))
                tmp.push(stringify(k) + ': ' + stringify(value[k]));
            }
            return '{' + tmp.join(', ') + '}';
          }
        }
        return '"' + value.toString().replace(escRE, escFunc) + '"';
      };
    })()
  };
}
```