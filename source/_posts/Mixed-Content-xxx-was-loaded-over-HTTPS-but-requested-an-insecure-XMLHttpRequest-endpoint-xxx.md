---
title: >-
  Mixed Content:xxx was loaded over HTTPS, but requested an insecure
  XMLHttpRequest endpoint xxx
top: false
cover: false
toc: true
mathjax: true
date: 2021-03-12 23:16:09
password:
summary: 在一个https的页面中，发送http请求，提示请求了一个不安全的脚本，报错Mixed Content
tags: [http,vue]
categories: [http,vue]
---

在一个https的页面中，发送http请求，提示请求了一个不安全的脚本，报错Mixed Content



https://blog.csdn.net/No_overtime_apes/article/details/101707562

页面的head中加入：
```html
<meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
```


https://blog.csdn.net/weixin_42207353/article/details/108271567

在我们服务器的响应头中加入：
```json
header("Content-Security-Policy: upgrade-insecure-requests");
```

vue的axios请求中添加请求头

```js
headers: {'Content-Security-Policy': 'upgrade-insecure-requests'}
```

```js
axios({
            method: "get",
            url: "http://xxxxxx",
            // url: "http://localhost:8080/dmb/exportExcel.xlsx",
            params: params,
            responseType: "blob",
            // 升级http请求为HTTPS请求，解决mixed content报错
            headers: {'Content-Security-Policy': 'upgrade-insecure-requests'}
          }).then((res) => {
          ····
          })
```

