---
title: es6 三点运算符_JavaScript ES6扩展运算符（...）用例
top: false
cover: false
toc: true
mathjax: true
date: 2021-07-31 11:56:47
password:
summary: es6 三点运算符_JavaScript ES6扩展运算符（...）用例
tags: ES6
categories: ES6
---

##### 作用一：

**在函数调用中，将剩余参数合并到一个数组中**

```js
function showName(firstName, lastName, ...titles) {
  console.log( firstName + ' ' + lastName ); // Julius Caesar
  // 剩余的参数被放入 titles 数组中
  // titles = ["Consul", "Imperator"]
  console.log( titles[0] ); // Consul
  console.log( titles[1] ); // Imperator 
  console.log( titles.length ); // 2
}
showName("Julius", "Caesar", "Consul", "Imperator")
function allName(...name) {
	console.log(name) // ["王", "二"]
}
allName('王','二')
```

##### 作用二：

**数组添加**

```js
let arr1 = [1,2,3]
let arr2 = [4,5,6]
arr1.push(...arr2)
console.log(arr1) // [1, 2, 3, 4, 5, 6]
```

##### 作用三：

**数组合并**

```js
let arr1 = ['a','b','c']
let arr2 = ['d','e','f']
let arr3 = ['h','i','j']
let allArr1 = arr1.concat(arr2,arr3)  // concat不会改变原数组
console.log(allArr1) // ["a", "b", "c", "d", "e", "f", "h", "i", "j"]
let allArr2 = [...arr1, ...arr2, ...arr3]
console.log(allArr2 ) // ["a", "b", "c", "d", "e", "f", "h", "i", "j"]
```

##### 作用四：

**将字符串装换为数组**

```js
let str = 'hello'
let arr = [...str]
console.log(arr) // ["h", "e", "l", "l", "o"]
```

##### 作用五：

获取数组最大值时修改数组数据类型传入Math.max

```
let arr = [3, 5, 1];
console.log(Math.max(arr))// NaN
console.log(Math.max(...arr)) // 5
```

##### 作用六： 

**对象合并**

```js
let obj1 = {
	a: 1,
	b: 2
}
let obj2 = {
	...obj1,
	c: 3
}
console.log(obj2) // {a: 1, b: 2, c: 3}
```

