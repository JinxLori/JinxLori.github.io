---
title: img 和 span 在一行显示，如何垂直居中？
top: false
cover: false
toc: true
mathjax: true
date: 2021-07-31 11:20:28
password:
summary: img 和 span 在同一行显示时，怎样达到垂直居中的效果(vertical-align:middle;)。多用于实现一些标签或者描述等...
tags: css
categories: css
---

#### img span在一行显示，如何垂直居中的问题 (vertical-align:middle;)

```html
<img src="img/info.png" alt="" />
<span>操作系统基本信息</span>
```

想让img和span在一行显示，并且垂直居中。如图所示。

<img src="https://img-blog.csdnimg.cn/20190410091829659.png" style="zoom: 150%;" />

只需要添加如下样式即可。

```css
img,span{
    vertical-align:middle;
}
```

