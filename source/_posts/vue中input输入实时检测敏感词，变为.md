---
title: vue中input输入实时检测敏感词，变为***
top: false
cover: false
toc: true
mathjax: true
date: 2021-02-02 14:49:40
password:
summary:
tags:
categories:
---

https://my.oschina.net/u/4405256/blog/4697807

```js
// 敏感词检测
export function checkSensitive(word) {
  console.log(word)
  const words = '赌博#嫖娼#卖淫#毒品#黄片#开赌六合彩' +
              '#操#草#操你妈#去你大爷#你妈逼#狗日' +
              '#台湾独立#香港独立#西藏独立#推翻共产党#李洪志#法轮功' +
              '#李源潮#王岐山#张德江#刘云山#刘奇葆#赵乐际#栗战书#杜青林#赵洪祝#张高丽#刘延东#江泽民#胡锦涛#温家宝#习近平#李克强'
  const sensitiveWordsArr = words.split('#')
  for (var i = 0; i < sensitiveWordsArr.length; i++) {
    const reg = new RegExp(sensitiveWordsArr[i], 'gi')
    if (word.indexOf(sensitiveWordsArr[i]) !== -1) {
      word = word.replace(reg, '***')
    }
  }
  return word
}
```



```js
checkSensitive(data) {
      this.formData.textarea = checkSensitive(data)
    },
```

```html
<el-input
            v-model="formData.textarea"
            type="textarea"
            rows="18"
            placeholder="输入直播间里需要发送的弹幕，每一行是一句。"
            @input="checkSensitive"
          />
```

