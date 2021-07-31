---
title: 'css---计算页面的的宽度和长度(width: calc(100% - 20px))'
top: false
cover: false
toc: true
mathjax: true
date: 2021-07-31 11:28:43
password:
summary: css
tags: css
categories: 有时候我们想要的就是里面的宽度是100%-20的宽度，很多时候我们会用JS来做，其实我们可以用css来做。
---

#### css---计算页面的的宽度和长度(width: calc(100% - 20px))

今天浏览这个http://www.sitepoint.com站时，因为好奇看了下人家写的代码，结果发现了这行代码，

![](https://img.jbzj.com/file_images/article/201803/2018322150209327.png?201822215222)

于是就研究了一下，calc()从字面我们可以把他理解为一个函数function。其实calc是英文单词calculate(计算)的缩写，是css3的一个新增的功能，用来指定元素的长度。比如说，你可以使用calc()给元素的border、margin、pading、font-size和width等属性设置动态值。为何说是动态值呢?因为我们使用的表达式来得到的值。不过calc()最大的好处就是用在流体布局上，可以通过calc()计算得到元素的宽度。

**calc()能做什么？
**

calc()能让你给元素的做计算，你可以给一个div元素，使用百分比、em、px和rem单位值计算出其宽度或者高度，比如说“width:calc(50% + 2em)”，这样一来你就不用考虑元素DIV的宽度值到底是多少，而把这个烦人的任务交由浏览器去计算。

**calc()语法
**

calc()语法非常简单，就像我们小时候学加 （+）、减（-）、乘（*）、除（/）一样，使用数学表达式来表示：

```
width``: calc(expression);
```

其中”expression”是一个表达式，用来计算长度的表达式。

**calc()的运算规则**

calc()使用通用的数学运算规则，但是也提供更智能的功能：

1. 使用“+”、“-”、“*” 和 “/”四则运算；
2. 可以使用百分比、px、em、rem等单位；
3. 可以混合使用各种单位进行计算；
4. 表达式中有“+”和“-”时，其前后必须要有空格，如”widht: calc(12%+5em)”这种没有空格的写法是错误的；
5. 表达式中有“*”和“/”时，其前后可以没有空格，但建议留有空格。

**浏览器的兼容性**

![img](https://img.jbzj.com/file_images/article/201803/2018322150309857.png?201822215319)

我们来个例子，我们做一个三列并排的模块，宽度按百分比、有padding值、有border值、还有margin-right，而且这三个值是px，

```
li{
float:left;
 
width:33.3333%;
height:50px;
 
padding:10px;
margin-right:10px;
 
background:#FF6666;
border:5px solid #DAC8A7;
}
```

效果图：

![img](https://img.jbzj.com/file_images/article/201803/2018322150358484.png?201822215410)

它是不会好好并列的，在这种情况下就不好算了，就算算出来也有那么一点误差，不是吗？现在我们就用到了calc(),

```css
li{
float:left;
 
//width:33.3333%;
height:50px;
 
padding:10px;
margin-right:15px;
 
background:#FF6666;
border:5px solid #DAC8A7;
 
width:calc(33.3333% - (10px + 5px) * 2 - 15px )
 
}
```

意思是(width-(padding+border)*2-margin)

现在可以并排了

![img](https://img.jbzj.com/file_images/article/201803/2018322150428118.png?201822215439)

好了，到这就告一段络了，再稍微优化一下左右边15px的空距，让两边都挨边。就在父级上加个margin-right：-15px，OK 搞定，

现在拿这个去做响应模式应该很方便了，

还有一篇外国人写的具体如何做大家有兴趣的可以了解一下http://osvaldas.info/imitating-calc-fallback-fixed-width-sidebar-in-responsive-layout

[相关资源](https://www.jb51.net/css/604657.html)