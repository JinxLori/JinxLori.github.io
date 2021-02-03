---
title: Django运行环境配置记录
top: false
cover: false
toc: true
mathjax: true
date: 2020-12-08 16:19:29
password:
summary: Django项目运行环境配置记录
tags: [Django]
categories: [Django]
---

### 环境配置：

1. #### 安装Python

   下载安装包，安装时勾选添加路径至环境变量， 或者手动配置。

   cmd 输入命令

   ```none
   Python
   ```

   验证成功

2. #### 安装Django

   ##### 通过pip安装Django

   cmd输入命令：

   ```bash
   $ pip install django
   ```

   如果下载速度慢，使用国内提供的安装源：

   ```bash
   $ pip install -i https://pypi.tuna.tsinghua.edu.cn/simple Django
   "-i" 指定单次安装源
   ```

   ##### 验证安装

   进入Python交互式环境

   输入命令：查看Django安装版本

	```bash
	>>> import django
	>>> django.get_version()
	```

	![](https://github.com/JinxLori/BlogImage/raw/master/2020_12_08/image-20201207164249014.png)
	
	或者使用`pip list`命令
	
	![](https://github.com/JinxLori/BlogImage/raw/master/2020_12_08/image-20201207164509590.png)
	
	##### 配置系统环境
	
	在Python解释器目录下的Scripts文件夹中可找到一个`django-admin.exe`文件，这是Django的核心管理程序，最好将它加入操作系统的环境变量
	
	![image-20201207164940758](https://github.com/JinxLori/BlogImage/raw/master/2020_12_08/image-20201207164940758.png)
	
	![](https://github.com/JinxLori/BlogImage/raw/master/2020_12_08/image-20201207165011180.png)
	
	cmd 直接输入命令，如图 则配置成功
	
	```bash
	django-admin help
	```
	
	![](https://github.com/JinxLori/BlogImage/raw/master/2020_12_08/image-20201207165117614.png)
	
3. #### 创建项目

4. #### 运行导入的项目或者Git的项目

   在项目的文件夹下面（含有manage.py）,打开命令行输入：

   ```bash
   python manage.py migrate
   ```

   ![](https://github.com/JinxLori/BlogImage/raw/master/2020_12_08/image-20201207172602453.png)

   因为库的缺失会出现一系列问题，下面记录一下我遇到的问题：在下载一些库时，速度较慢，需要用到上面安装Django时的数据源。Django换成install后面的库名称即可

   ```none
   $ pip install -i https://pypi.tuna.tsinghua.edu.cn/simple Django
   ```

   ##### 问题：

   问题一：

   ```bash
   ModuleNotFoundError: No module named 'corsheaders'
   ```

   ```none
   pip install django-cors-headers
   ```

   问题二：

   ```bash
   ModuleNotFoundError: No module named 'adminlte3'
   ```

   ```bash
   pip install django-adminlte3
   ```

   问题三：

   ```bash
   ModuleNotFoundError: No module named 'drf_yasg'
   ```

   ```bash
   pip install drf_yasg
   ```

   问题四：

   ```bash
   ModuleNotFoundError: No module named 'rest_registration'
   ```

   ```bash
   pip install django-rest-registration
   ```

   问题五：

   ```bash
   ModuleNotFoundError: No module named 'django_filters'
   ```

   ```bash
   pip install django-filter
   ```

   问题六：

   ```bash
   ModuleNotFoundError: No module named 'rest_framework_simplejwt'
   ```

   ```bash
   pip install djangorestframework-simplejwt
   ```

   最后成功效果图：

   ![](https://github.com/JinxLori/BlogImage/raw/master/2020_12_08/image-20201207173505632.png)

5. #### 运行Django项目;

   输入一下命令。可以是cmd中输入，也可以编译器打开控制台输入

   ```bash
   python manage.py runserver
   ```

   ![](https://github.com/JinxLori/BlogImage/raw/master/2020_12_08/image-20201207174347066.png)
