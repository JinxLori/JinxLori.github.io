---
title: android程序因图片或者其他资源过大，内存分配不足解解决
top: false
cover: false
toc: true
mathjax: true
date: 2021-02-01 16:26:56
password:
summary:
tags: Android
categories:
---

https://stackoverflow.com/questions/32244851/androidjava-lang-outofmemoryerror-failed-to-allocate-a-23970828-byte-allocatio

报错内容：

```bash
Android:java.lang.OutOfMemoryError: Failed to allocate a 23970828 byte allocation with 2097152 free bytes and 2MB until OOM
```

解决办法：

`android:largeHeap="true"`

```xml
<application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher1"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme"
        android:largeHeap="true">
```

