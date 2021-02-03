---
title: vue接受base64转图片验证码
top: false
cover: false
toc: true
mathjax: true
date: 2020-12-28 16:19:29
password:
summary: vue接受后台base64编码转图片验证码并在前端页面显示
tags: [vue]
categories: [vue]
---

### 前言：

开发过程中，如登录注册页面表单等会需要图形验证码，前端获取到后台返回的Base64图片编码，将其解码为file文件，在实现对该file文件的加载与预览。

### 步骤：

1. 编写解码函数`base64ImgtoFile('data:image/png;base64,XXXXX...')`
2. 使用`URL.createObjectURL`将图片转换为临时路径
3. 使用img标签加载临时路径的图片

base64ImgtoFile可以封装为公共组件放在utils文件夹的global.js中

### 封装方法 base64ImgtoFile()：

```js
export function base64ImgtoFile(dataurl, filename = 'file') { 
    let arr = dataurl.split(',') 
    let mime = arr[0].match(/:(.*?);/)[1] 
    let suffix = mime.split('/')[1] 
    let bstr = atob(arr[1]) 
    let n = bstr.length 
    let u8arr = new Uint8Array(n) 
    while (n--) { 
        u8arr[n] = bstr.charCodeAt(n) 
    } 
    return new File([u8arr], `${filename}.${suffix}`, { 
        type: mime 
    }) 
}
```

### 组件中引用 base64ImgtoFile：

```js
import { base64ImgtoFile } from "@/utils/global"; 

// base64编码的图片 
var base64Img = 'data:image/png;base64,XXXXX...'; 
//转换图片文件 
var imgFile = base64ImgtoFile(base64Img);
```

### 图片File文件加载预览：

使用`URL.createObjectURL`将图片转换为临时路径,并赋值给img标签



#### img标签：

```js
<el-form-item style="position: relative" prop="captcha"> 
    <el-input 
		v-model="registerForm.captcha" 
		name="logVerify" 
		placeholder="请输入图形验证码" 
		style="width: 60%" /> 
    <div class="vPic"> 
        <img 
			v-if="picPath" 
			:src="picPath" 
			width="100%" 
			height="100%" 
			alt="请输入验证码" 
			@click="loginVefify()" /> 
    </div> 
</el-form-item>
```

#### File转换为路径：

使用img标签加载临时路径的图片

```js
var file = base64ImgtoFile(ele.data); 
// ele.data 为接受的Base64格式编码 eg: 'data:image/png;base64,XXXXX...'
var imgurl = URL.createObjectURL(file);
this.picPath = imgurl;
```

