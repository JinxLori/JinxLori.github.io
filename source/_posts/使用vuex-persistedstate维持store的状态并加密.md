---
title: 使用vuex-persistedstate维持store的状态并加密
top: false
cover: false
toc: true
mathjax: true
date: 2021-01-07 16:19:29
password:
summary: vue中store会随页面刷新而丢失，使用persistedstate维持store的状态并使用secure-ls加密
tags: [vue]
categories: [vue]
---

在使用vue时，我们常会利用vuex来集中管理组件的状态，例如用户登录状态，用户授权状态，又或者是其他的页面信息以及状态。但是当我们刷新页面，存在store/state中的信息就会被清空，为了用户体验以及请求开销，我们需要使用客户端来暂时存储这些信息，如localstorage，cookie等。而不需要去重新向服务器发送获取信息的请求。

### 使用 vuex-persistedstate 套件將状态存入 localStorage

#### store中引入：

```js
import VuexPersistence from 'vuex-persist' 

const vuexLocal = new VuexPersistence({ 
    storage: window.localStorage, 
    modules: ['user'] // 存入localstorage的key 
}) 
export const store = new Vuex.Store({ 
    modules: { 
        user, 
        router, 
        dictionary 
    }, 
    plugins: [vuexLocal.plugin] 
})
```

可以看到，store实例中比平时多一个`plugins: [vuexLocal.plugin]`，其余跟平常的store用法一样，存state，获取state。

但是这些信息赤裸裸的放在这里不好，如果想要加密localstorage中的信息可以使用secure-ls

### secure-ls 加密 localStorage：

#### npm安装secure-ls：

```bash
npm install secure-ls
```

#### store中引入：

修改之前的VuexPersistence实例就OK了

```js
const vuexLocal = new VuexPersistence({
    // storage: window.localStorage,
    // modules: ['user']
    
    key: "user", //儲存在 localStorage 的 key
      storage: {
        getItem: key => ls.get(key),
        setItem: (key, value) => ls.set(key, value),
        removeItem: key => ls.remove(key)
      }
})
```

### 详细内容进阶：

[vuex-persistedstate](https://github.com/robinvdvleuten/vuex-persistedstate)
[secure-ls](https://www.npmjs.com/package/secure-ls)

#### 参考网址：

> https://github.com/robinvdvleuten/vuex-persistedstate
>
> https://www.npmjs.com/package/secure-ls
>
> https://blog.csdn.net/qq_32674347/article/details/105807542
>
> [https://chiafangsung.medium.com/%E4%BD%BF%E7%94%A8-vuex-persistedstate-%E7%B6%AD%E6%8C%81-vuex-%E7%8B%80%E6%85%8B-f0d7c522c73a](https://chiafangsung.medium.com/使用-vuex-persistedstate-維持-vuex-狀態-f0d7c522c73a)

