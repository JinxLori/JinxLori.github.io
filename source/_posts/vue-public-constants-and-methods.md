---
title: vue public constants and methods
top: false
cover: false
toc: true
mathjax: true
date: 2020-12-17 15:13:55
password:
summary: vue 公共常量以及方法的使用
tags: vue
categories: vue
---

在使用vue的过程中，会遇到一些可以复用或者多次调用的常量以及函数方法，为了减小代码量以及后期的维护，可以将这些常量方法实现共用。

方法有很多，这里记录一种自己比较常用的。

##### 在src文件夹下创建utils文件夹

##### 在utils中新建一个global.js的文件

该文件夹中放入共用的常量以及方法，并export出来，如下

`global.js `

```js
const emojiArray = ['[微笑]', '[害羞]', '[击掌]', '[握手]', '[爱心]', '[调皮]', '[礼物]', '[派对]', '[嘿哈]', '[悠闲]',
  '[憨笑]', '[太阳]', '[猪头]', '[送心]', '[耶]', '[大笑]', '[小鼓掌]', '[偷笑]', '[愉快]', '[飞吻]', '[呲牙]', '[拳头]', '[发]'
]

function getRandomEmojiIndex() { // 获取随机的emoji表情
  return Math.floor(Math.random() * emojiArray.length) // 可均衡获取 0 到 22 的随机整数。
}

function getRandomEmojiNum() { // 获取添加的emoji表情数量 1-5
  return Math.floor(Math.random() * 5) + 1 // 可均衡获取 1 到 5 的随机整数。
}


// 将方法通过export 让其他组件import访问
export function getEmojiStr() { // 结合上面两个随机方法获得一个emoji字符串
  var emojiStr = ''
  var num = getRandomEmojiNum()
  console.log('num:', num)
  for (var i = 0; i < num; i++) {
    var index = getRandomEmojiIndex()
    console.log('index:', index)
    emojiStr = emojiStr + emojiArray[index]
  }
  return emojiStr
}

// 我这个项目中没用到这个，所以注释。
// 将常量通过export 让其他组件import访问
// export default {
//   emojiArray
// }

```

##### 组件中import常量或者方法

```js
import { getEmojiStr } from '@/utils/global'
```

##### 组件中使用该常量或者方法

```js
var emojiStr = getEmojiStr()
console.log(emojiStr)
```

