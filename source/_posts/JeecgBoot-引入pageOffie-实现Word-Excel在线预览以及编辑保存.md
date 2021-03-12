---
title: 'JeecgBoot 引入pageOffie 实现Word,Excel在线预览以及编辑保存'
top: false
cover: false
toc: true
mathjax: true
date: 2021-03-12 15:30:13
password:
summary: jeecgBoot结合pageoffice在线预览Word，Excel以及编辑保存
tags: [jeecgboot,pageoffice]
categories: [jeecgboot,pageoffice]
---

https://blog.csdn.net/las723/article/details/86503557

https://gitee.com/zhengqingya/java-workspace/tree/master/Spring%20Boot%20%E7%B3%BB%E5%88%97/SpringBoot(30)%20%E6%95%B4%E5%90%88PageOffice%E5%AE%9E%E7%8E%B0%E5%9C%A8%E7%BA%BF%E7%BC%96%E8%BE%91Word%E5%92%8CExcel



将上面的代码作为模块包加入jeecgboot项目

![image-20210312153418413](C:\Users\念一\AppData\Roaming\Typora\typora-user-images\image-20210312153418413.png)

在system的模块中的主程序jeecgApplicatoion.java中添加以下代码，创建所需文件的路径。

```java
//  @Value("${pageoffice.posyspath}")
//  private String poSysPath;

  /**
   * 添加PageOffice的服务器端授权程序Servlet（必须）
   *
   * @return
   */
  @Bean
  public ServletRegistrationBean servletRegistrationBean() {
    com.zhuozhengsoft.pageoffice.poserver.Server poserver = new com.zhuozhengsoft.pageoffice.poserver.Server();
    // 设置PageOffice注册成功后,license.lic文件存放的目录
    poserver.setSysPath("D:\\Project\\档案管理系统\\File_Management\\pageoffice\\pageoffice\\lic/");
    ServletRegistrationBean srb = new ServletRegistrationBean(poserver);
    srb.addUrlMappings("/poserver.zz");
    srb.addUrlMappings("/posetup.exe");
    srb.addUrlMappings("/pageoffice.js");
    srb.addUrlMappings("/jquery.min.js");
    srb.addUrlMappings("/pobstyle.css");
    srb.addUrlMappings("/sealsetup.exe");
    return srb;
  }
```

该代码之前位于pageOffice模块中的controller中，添加为jeecg的模块之后，不会去执行该Bean类，所以需要提放至主程序中执行。

否则会获取不到对应的路径，如pageoffice.js等



将pageoffice模块中的application.yml中的配置提放至system中的application.yml文件中，否则跟上述的代码一样读取不到



去掉pageoffice模块中的config文件夹以及其中的拦截器配置，不然会提示与jeecgboot的冲突



最后还需要将pageoffice模块中java的包路径更改为org.jeecg.modules

![image-20210312155535184](C:\Users\念一\AppData\Roaming\Typora\typora-user-images\image-20210312155535184.png)

 



测试：

将pageoffice模块中的index.html的代码复制放入vscode中，可以新建test.html，或者直接用vscode打开index.html

