---
title: '在el-row中循环渲染el-col,希望自动换行，el-col数据为空时，布局混乱'
top: false
cover: false
toc: true
mathjax: true
date: 2021-07-31 10:42:41
password:
summary: 在一个el-row标签中渲染多个el-col，希望能够达到自动换行的效果，当el-col没有数据时，布局会变得混乱.
tags: [Element,Vue]
categories: [Element,Vue]
---

#### 使用ElementUI的el-row，渲染多行的el-col，当数据为空时，布局显示混乱的解决方案

##### 问题：

大家可能在使用el-row el-col进行布局的时候，可能会出现没有数据，el-col没有占位，

##### 解决方案：

因为有些人为了简单，把所有的el-col放在一个el-row内，如果只有**display:flex**，会把所有的el-col都挤在一行。

加上**flex-wrap: wrap**之后可以自动换行，和分开写在el-row每一行的一样。

```css
.el-row{
    display:flex;
    flex-wrap: wrap;
}
//加flex-wrap: wrap;因为有些人为了简单，把所有的el-col放在一个el-row内，如果只有display:flex;会把所有的el-col都挤在一行。加上flex-wrap: wrap;之后可以自动换行，和分开写在el-row每一行的一样。
```

##### 参考网址：

[参考网址](https://www.freesion.com/article/80161191468/)