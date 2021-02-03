---
title: Genymobile/scrcpy Android USB
top: false
cover: false
toc: true
mathjax: true
date: 2020-12-16 16:19:29
password:
summary: 开源免费在电脑显示手机画面并控制手机的工具
tags: [Android, tool]
categories: [Android, tool]
---

### scrcpy简介：

此项目为开源项目，Github地址：[Genymobile/scrcpy: Display and control your Android device](https://github.com/Genymobile/scrcpy)

Windows 下载：[scrcpy-win64-v1.16.zip](https://link.zhihu.com/?target=https://github.com/Genymobile/scrcpy/releases/download/v1.16/scrcpy-win64-v1.16.zip)

### scrcpy使用：

#### usb投屏：

电脑端完成配置后，我们还需要在手机端开启 `开发者选项` 及 `USB 调试`。然后使用数据线将手机和电脑连接并允许 USB 调试，双击解压得到的 **scrcpy.exe** 文件，即可进行有线投屏。

#### 无线投屏：

1. 确保 PC 和手机处于同一局域网中
2. 打开 PowerShell (~ cmd)，依次操作并输入代码

```bash
# a.将代码目录定位到 scrcpy 文件夹 
cd D:\Libraries\Desktop\scrcpy-win64-v1.16​

# b.在手机端开启「开发者选项」及「USB 调试」，然后使用数据线将手机和电脑连接并允许 USB 调试，开启手机端口 # 如果本行显示 no device 或未启动 adb，需检查「USB 调试」是否开启。 # 此外，一些手机需选择「文件传输」模式方能使用 adb。 
.\adb tcpip 5555​

# c.拔出手机数据线，开始无线投屏。(192.168.2.234 为手机端 ip，需更改) 
.\adb connect 192.168.2.234:5555​

# d.启动 scrcpy.exe 
.\scrcpy 

# 如有报错，可启动低分辨率投屏 
.\scrcpy -m 1920
```

手机IP可通过手机的`状态信息`查看

正如预期的那样，性能与USB不同，默认的scrcpy比特率是8Mbps，这对于Wi-Fi连接来说可能太多了。根据使用情况，降低比特率和分辨率可能是一个很好的折中方案。

```bash
scrcpy --bit-rate 2M --max-size 800
# 或者简写
scrcpy -b2M -m800
```

