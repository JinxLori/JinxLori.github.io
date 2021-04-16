---
title: Vue 常用知识
top: false
cover: false
toc: true
mathjax: true
date: 2021-04-16 13:24:35
password:
summary: Vue 面试高频率问题集合
tags: Vue
categories: Vue
---

#### let ,var ,const 之间的区别

var声明变量可以重复声明，而let不可以重复声明

const声明之后必须赋值，否则会报错
const定义不可变的量，改变了就会报错

const和let一样不会与window相映射、支持块级作用域



#### 父子组件的传值

父组件**传值**给子组件：
第一步：在父组件中 **v-bind:parentmsg**=“父组件的data值”（parentmsg 这个名字可自定义）
第二步：在子组件中 **props:[‘parentmsg’] ** ，{{parentmsg}}这样就可以使用 父组件的值

父组件把**方法**传递给子组件：
第一步：在父类组件中 **@func**=父组件方法名 (方法名不带‘()’,func可自定义)
第二步：在子组件方法中写 **this.$emit(‘func’,方法参数)** (func可自定义，无参方法‘方法参数’就别写)



#### 路由跳转的方式

```js
<router-link to='home'> router-link
router.push('/home')
```



#### vue-router 中 hash 模式和 history 模式的区别

最直观的区别是在 url 中 **hash 带了一个 #** 而 history 是没有的；

history 需要后端提供支持；
history 跳转后刷新或者回跳会报错



#### axios 怎样发送请求

get请求，参数是放到params属性中

```js
//指定基本url默认配置
axios.defaults.baseURL = 'http://localhost:8888'
 
//默认是get请求方式，可以不用指定
axios({
    //这里的url路径是不能取消 / 的，因为路径必须带
    url: '/user',
    params:{
        id: 1
    }
}).then(response => {
                    console.log(response.data)
                    })
```

post一定要指定，注意数据是放在data属性中的，而不是params中

```js
post一定要指定，注意数据是放在data属性中的，而不是params中

axios({
    url: '/user',
    method: 'post',//这里既可以大写也可以小写，最终底层代码中都会转为大写
    data: {
        "title": "js"
    }
})
```



#### 计算属性（computed）和 watch 的区别

简单来说computed是计算值，**只有值发生变化才会执行方法**，watch是监听观察动作，**有改变就执行**，

**computed具有缓存性**，数据变化时先读取缓存，**值没变这不做操作**，而**watch没有缓存**，**直接执行**。



#### Get 请求和 Post 请求的区别

**Get是不安全的**，因为在传输过程，数据被放在请求的URL中；Post的所有操作对用户来说都是不可见的。

**Get传送的数据量较小**，这主要是因为受URL长度限制；Post传送的数据量较大，一般被默认为不受限制

**Get限制Form表单的数据集的值必须为ASCII字符**；而Post支持整个ISO10646字符集。

**Get执行效率却比Post方法好**。Get是form提交的默认方法。



#### 列举css 选择器及优先级

1. **html**标记选择器。

   指用html的标记语言作为选择器, 如：ｐ｛｝、　ｂ｛｝、　ｈ1 { } 等等。 

2. **id**选择器。

   id选择器是指用指定的id name作为选择器。 例如 如果要选择id=“one”的元素，选择器就是： #one { }。 

3. **类**选择器。

   类选择器是指用一个类（class）的name来作为选择器。 例如，b元素和p元素都被归为“two”类（class=“two”）的话，选择器就是： .two { }  /* 不能忘记前面的小点*/

4. **组合**选择器

   把多个元素组合在一起选择。p, b , h1 { }           /*标记之间用逗号*/

5. **关联**选择器，

   是指用两个多个标记进行特定的选择。例如，p元素里面有a元素，p元素之外也有a元素，想特定选择p里面的a元素的话 就可以写选择器：ｐ a { }    /* 中间用空格隔开*/

6. **伪类**选择器。

   伪类只用于a元素和p元素。

   

在**单个标签**的选择器中： **id > class > 标签(如p{})**

**!important**是无条件优先级，享有最高优先级，但是IE6不支持此属性。 

直接在html给元素添加**style的优先级位于第二高**。

最低一级的是用**通配选择器**。 *{ }。

当比较拥有相同级别的选择器的时候，定义的位置将决定一些。 



#### 简述 cookies sessionStorage 和 localStorage 区别

![img](https://images2018.cnblogs.com/blog/1287779/201804/1287779-20180404065845701-1111813120.png)



#### 数组去重

一般的数组去重可以直接用 new Set() 方法即可，但是数组对象的话，比较复杂，不能直接用，我们可以采取间接的方法来去重

```js
unique(arr) { //  arr为待去重的数组对象
 const res = new Map();
 return arr.filter((arr) => !res.has(arr.id) && res.set(arr.id, 1))
}
```



#### 判断一个字符串中出现次数最多的字符，统计这个次数、

```js
var str = 'asdfssaaasasasasaa';
var json = {};
for (var i = 0; i < str.length; i++) {
    if(!json[str.charAt(i)]){
       json[str.charAt(i)] = 1;
    }else{
       json[str.charAt(i)]++;
    }
};
var iMax = 0;
var iIndex = '';
for(var i in json){
    if(json[i]>iMax){
         iMax = json[i];
         iIndex = i;
    }
}        
console.log('出现次数最多的是:'+iIndex+'出现'+iMax+'次');
```



#### 把URL参数解析为一个对象

```tex
http://www.baidu.com?key0=0&key1=1&key2=2
```

```js
function parseQueryString(url) {
		   var params = {};
		   var arr = url.split("?");
		   if (arr.length <= 1) {
		      return params;
		   }
		   arr = arr[1].split("&");
		   for(var i = 0, l = arr.length; i < l; i++) {
		      var a = arr[i].split("=");
		      params[a[0]] = a[1];
		   }
		   return params;
	}
```



#### 简述Vue的响应式原理

当一个Vue实例创建时，vue会遍历**data选项的属性**，用 **Object.defineProperty** 将它们转为getter/setter并且在内部追踪相关依赖，在属性被访问和修改时通知变化。

每个组件实例都有相应的watcher程序实例，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的setter被调用时，会通知watcher重新计算，从而致使它关联的组件得以更新。



#### Vue中给data中的对象属性添加一个新的属性时会发生什么，如何解决？

示例：

![image-20210416124938831](C:\Users\念一\AppData\Roaming\Typora\typora-user-images\image-20210416124938831.png)

![image-20210416125002582](C:\Users\念一\AppData\Roaming\Typora\typora-user-images\image-20210416125002582.png)

点击button会发现， obj.b 已经成功添加，但是**视图并未刷新**

原因在于在Vue实例创建时， **obj.b 并未声明**，因此就没有被Vue转换为响应式的属性，自然就不会触发视图的更新，这时就需要使用Vue的全局api—— **$set()：**

```js
addObjB () {
      // this.obj.b = 'obj.b'
      this.$set(this.obj, 'b', 'obj.b')
      console.log(this.obj)
    }
```

**$set()** 方法相当于手动的去把 obj.b **处理成一个响应式的属性**，此时视图也会跟着改变了



#### 如何优化SPA应用的首屏加载速度慢的问题？

将公用的JS库通过script标签**外部引入**，减小 app.bundel 的大小，让浏览器并行下载资源文件，提高下载速度；

在配置 路由时，**页面和组件使用懒加载的方式引入**，进一步缩小 app.bundel 的体积，在调用某个组件时再加载对应的js文件；

加一个**首屏loading图**，提升用户体验；



#### jQuery获取的dom对象和原生的dom对象有何区别？

js原生获取的dom是一个对象，jQuery对象就是一个数组对象



#### 前端如何优化网站性能？

减少 HTTP 请求数量

控制资源文件加载优先级

利用浏览器缓存

减少重排（Reflow） 减少Reflow，如果需要在DOM操作时添加样式，尽量使用增加class属性，而不是通过style操作样式。

减少 DOM 操作

图标使用 IconFont 替换



#### key主要是解决哪一类的问题，为什么不建议用索引index（重绘）

key的作用主要是为了高效的更新虚拟DOM

当以index为key值时，如果数组长度发生变化，会导致key的变化，比如删除其中某一项，那么index会相应变化。
所以**用index作为key和不加key没有什么区别，都不能提升性能**。一般用每项数据的**唯一值**来作为key，就算数组长度变化，也不会影响到这个key



#### vue中如何编写可复用的组件

（1）以组件功能命名
（2）只负责ui的展示和交互动画，**不要在组件里与服务器打交道**（获取异步数据等）
（3）可复用组件不会因组件使用的位置、场景而变化。**尽量减少对外部条件的依赖。**



#### 完整的 vue-router 导航解析流程

https://zhuanlan.zhihu.com/p/99199175



#### vue-router的几种实例方法以及参数传递

router.push

<router-link>

**和name配对的是params，**  刷新页面参数丢失

**和path配对的是query**,  刷新页面参数不丢失  地址栏携带参数

```js
this.$router.push({ name: 'news', params: { userId: 123 }}); // **刷新页面参数会丢失**
this.$router.push({ path: '/news', query: { userId: 123 }}); // **刷新页面数据不会丢失**
```

1.命名路由搭配params，**刷新页面参数会丢失**

2.查询参数搭配query，**刷新页面数据不会丢失**  因为地址栏携带参数

3.接受参数使用this.$router后面就是搭配路由的名称就能获取到参数的值



#### vue-router如何定义嵌套路由？

children

```
const router = new VueRouter({
  routes: [
    { path: '/testPage', 　　　 component: testPage,
      children: [
        {
          path: '/sonPageA',
          component: sonPageA
        },
        {
          path: '/sonPageB',
          component: sonPageB
        }， 
      ]
    }，
    {
        // 其他和testPage平级的路由
    }
  ]
})
```



#### vue-router如何实现路由懒加载（ 动态加载路由 ）

https://blog.csdn.net/xm1037782843/article/details/88225104



#### router的meta有什么用

在meta对象中可以**设置一些状态**，通常设置标题或是否需要缓存。$route.meta.keepAlive/$route.meta.title

```js
{
    path:"/test",
    name:"test",
    component:()=>import("@/components/test"),
    meta:{
        title:"测试页面", //配置title
        keepAlive: true //是否缓存
    }
}
```

