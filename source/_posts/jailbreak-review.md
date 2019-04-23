---
title: 【iOS 逆向之旅】工具介绍篇
toc: true
date: 2019-04-21 22:05:58
tags: 
    - jailbreak
    - iOS
categories: iOS 逆向
---
# 越狱
## [Can I Jailbreak?](http://canijailbreak.com/)
# IPA 安装
## [Cydia Impactor](http://www.cydiaimpactor.com/)
# 砸壳
## [stefanesser dumpdecrypted](https://github.com/stefanesser/dumpdecrypted)
通过手动注入然后启动应用程序在内存进行dump解密后的内存实现砸壳，这种砸壳只能砸主App可执行文件。
## [conradev dumpdecrypted](https://github.com/conradev/dumpdecrypted)
对于应用程序里面存在framework的情况可以使用此中砸壳，通过_dyld_register_func_for_add_image注册回调对每个模块进行dump解密。
## [Clutch](https://github.com/KJCracks/Clutch)
对于含有 watchOS app 的应用，可能会砸壳失败。
## [frida-ios-dump](http://www.alonemonkey.com/2018/01/30/frida-ios-dump/)
终极砸壳工具，推荐使用此种砸壳方式。使用时需要先安装如下工具：
### [frida](https://www.frida.re/docs/home/)
1. Mac 安装 frida (python pip 工具安装)
    ```bash
    pip install frida
    pip install frida-tools
    ```
2. 越狱手机Cydia安装 frida
   Cydia 添加 `https://build.frida.re/` source，搜索 frida 安装。

### [usbmuxd](https://cgit.sukimashita.com/usbmuxd.git/) 
usb 端口转发工具
Install：`brew install usbmuxd`
Usage: `iproxy 2222 22`

`iproxy 2222 22`命令就是把当前要连接设备的22端口(ssh端口)映射到电脑的2222端口，那么想和设备22端口通信，直接和本地的2222端口通信就可以了。
以前的连接方式：
```bash
ssh -p 22 root@30.208.32.1731
#或者这样
ssh root@30.208.32.173 #ssh端口号默认22，可以不写
```
现在的连接方式:
```bash
ssh -p 2222 root@127.0.0.1
```

# 头文件导出
## [class-dump](https://github.com/nygard/class-dump)
# 可执行文件信息查看
## [MachOView](https://github.com/gdbinit/MachOView/) 
# 反汇编工具
## [IDA](https://www.hex-rays.com/products/ida/)
## [Hopper](https://www.hopperapp.com/)
[MachOView Download](https://sourceforge.net/projects/machoview/)
# 越狱插件编写
## [theos](https://github.com/theos/theos)
## [MonkeyDev](https://github.com/AloneMonkey/MonkeyDev)
# App 界面调试
## [Reveal](https://revealapp.com/)
# 系统文件管理
## [iFunbox](http://www.i-funbox.com/zh-cn_index.html?userchoose)
# 越狱手机插件安装
## [Dropbear](https://matt.ucc.asn.au/dropbear/dropbear.html)
  针对 iOS10 越狱后无法通过 [SSH 连接](https://zhuanlan.zhihu.com/p/34003393)。
## [Apple File Conduit 2](https://cydia.saurik.com/package/com.saurik.afc2d/)
## [Filza](https://filza.net/)