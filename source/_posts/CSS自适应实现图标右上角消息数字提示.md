---
title: CSS自适应实现图标右上角消息数字提示
top: false
cover: false
toc: true
mathjax: true
date: 2021-07-31 11:56:47
password:
summary: CSS自适应实现图标右上角消息数字提示,实现右上角的角标展示。
tags: css
categories: css
---

#### CSS自适应实现图标右上角消息数字提示,实现右上角的角标展示。

效果如下：一共改过两次

##### 改后

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190725103545383.png)

------

##### 改前：存在的问题

当数值为一位数时，底部应该是一个完整的圆形
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190725101646763.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190725101711663.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190725101718772.png)

##### 代码

```html
//改前
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <style>
            .msg {
                position: relative;
                width: 60px;
                height: 60px;
                margin: 60px;
				float:left;
            }
            .msg img {
                width: 60px;
                height: 60px;
            }
            .alarm {
                position: absolute;
                color: white;
                font-size: 17px;
                background-color: red;
                /*height: 24px;改前*/
                min-height: 24px;/*改后新增的代码*/
				min-width:24px;/*改后新增的代码*/
                line-height: 24px;
                right:-12%;
                top: -12px;
                text-align: center;
				 -webkit-border-radius: 24px;
                border-radius: 24px;
				padding:2px;
            }
        </style>
    </head>
    <body>
        <div class="msg">
            <img src="img/1.png" />
            <div class="alarm">
               50000
            </div>
        </div>
    </body>
</html>
```

[相关资源](https://blog.csdn.net/qq_36337754/article/details/97240414)