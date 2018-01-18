---
title: Javascript toString() toLocaleString()
date: 2018-01-18 05:30:09
categories:
- Javascript
tags:
- js
---

### 一、JS Array

toString()：把数组转换为字符串，并返回结果，每一项以逗号分割。

toLocalString()：把数组转换为本地数组，并返回结果。

### 二、JS Date

```javascript
var date = new Date();
console.log(date.valueOf());
console.log(date.toString());
console.log(date.toLocaleString());
```
![img01](/assets/images/data_1.png)

valueOf：返回 Date 对象的原始值，以毫秒表示。

toString()：把 Date 对象转换为字符串，并返回结果。使用本地时间表示。

toLocalString()：可根据本地时间把 Date 对象转换为字符串，并返回结果，返回的字符串根据本地规则格式化
### 三、JS Number
```javascript
var num = new Number(1337);
console.log(num.valueOf());
console.log(num.toString());
console.log(num.toLocaleString());
```
![img02](/assets/images/data_2.png)
valueOf：返回一个 Number 对象的基本数字值。

toString()：把数字转换为字符串，使用指定的基数。

toLocalString()：把数字转换为字符串，使用本地数字格式顺序。

### 四、toString()方法与toLocalString()方法区别：

* toLocalString()是调用每个数组元素的 toLocaleString()
方法，然后使用地区特定的分隔符把生成的字符串连接起来，形成一个字符串。

* toString()方法获取的是String(传统字符串),而toLocaleString()方法获取的是LocaleString(本地环境字符串)。
如果你开发的脚本在世界范围都有人使用，那么将对象转换成字符串时请使用toString()方法来完成。

* LocaleString()会根据你机器的本地环境来返回字符串，它和toString()返回的值在不同的本地环境下使用的符号会有微妙的变化。

所以使用toString()是保险的，返回唯一值的方法,它不会因为本地环境的改变而发生变化。如果是为了返回时间类型的数据，推荐使用LocaleString()。若是在后台处理字符串，请务必使用toString()。
