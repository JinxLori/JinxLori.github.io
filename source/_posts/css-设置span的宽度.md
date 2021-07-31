---
title: css 设置span的宽度
top: false
cover: false
toc: true
mathjax: true
date: 2021-07-31 10:10:05
password:
summary: 在默认的情况下，利用css样式对span进行宽度设定是无效，但有时为了某种排版的要求，需要对span进行宽度设定，那么如何在html中利用css样式设定span的宽度？
tags: css
categories: css
---

#### 问题：

在默认的情况下，利用css样式对span进行宽度设定是无效，但有时为了某种排版的要求，需要对span进行宽度设定，那么如何在html中利用css样式设定span的宽度？

#### 思路：

这看上去是个很简单的问题，似乎用style中的width属性就可以。

然而通过试验以后发现，无论是在Firefox还是IE中都无效

在css2的标准中，查阅关于width的定义，我们可以发现，原来css中的width属性并不总是有效的，**如果对象是inline对象**，width属性就会被忽略。Firefox和IE都遵循了这个标准。

#### 解决：

##### 方案1：将span转为块状标签，使用block

```css
span { 
	display:block; 
	width:150px; 
}
```

这样宽度就可以实现了，**不过这样做也把前后文字隔在不同行里面**。这样其实span就完全变成了div。

##### 方案二： 解决方案一中，不同span在不同行的问题，既换行问题。

```
span { 
	display:block; 
	float:left;
	width:150px; 
}
```

但如果span前面没有文字，那的确是可行的。但是如果有了，前后文字就会连在一起，而span跑到了第二行。



其实，在Html的各种Element中，的确有**既是inline，又能够设定宽度的情况存在**。例如button对象，就可以很好的在文字中间出现，并且设定宽度。

能不能让span象button那样显示呢？通过css2标准中display的定义和inline对象的解释，发现css2标准的制定者把所有的Element在是否属于inline上做了非此即彼的规定，要么是inline，要么是block，没有制定button那样既是inline，又可以象block那样设置宽度的属性值。

在css2.1标准草案中display的定义中增加了一个叫**inline-block**的属性值，针对的恰好是我们面对的这种情形。那么再看看各种浏览器的对应情况。

Firefox：通过display的文档了解到，inline-block在未来的Firefox 3中会实现。通过Mozllia扩展属性参考了解到，在Firefox 3以前的版本，例如现在的Firefox 2中，可以用-moz-inline-box达到同样的效果。

IE：通过MSDN中的display文档了解到，inline-block已经实现。实际测试发现IE 6.0以后都没问题。

##### 完美的解决span宽度问题的方案：inline-block

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" >
<head>
	<title>Test Span</title>
	<style type="text/css">
		span {
				display:-moz-inline-box;
				display:inline-block;
				width:150px; 
			}
	</style>
</head>
<body>
	HCONLY视觉网站设计<span>width</span>营销策划
</body>
</html>
```

