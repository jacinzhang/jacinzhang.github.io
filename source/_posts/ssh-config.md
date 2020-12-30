---
title: 【工具配置】SSH 配置
toc: true
date: 2019-07-14 12:23:31
tags: 
 - SSH 
 - shell
categories: 网络
---
> 背景：今天配置了 `git` 代理的时候，碰到 `SSH` 方面的一些配置问题，查阅后在此记录下。

[SSH (Secure Shell)](https://zh.wikipedia.org/zh-cn/Secure_Shell) 是什么？是一项创建在应用层和传输层基础上的安全协议，为计算机上的 Shell（壳层）提供安全的传输和使用环境。也是专为远程登录会话和其他网络服务提供安全性的协议。它能够有效防止远程管理过程中的信息泄露问题。通过 SSH 可以对所有传输的数据进行加密，也能够防止 DNS 欺骗和 IP 欺骗。

本篇文章主要介绍 `SSH` 相关的使用技巧。通过对 `~/.ssh/config` 文件的配置你可以大大简化 `SSH` 相关的操作。

# 配置文件

`SSH` 程序可以从以下途径获取参数：
1. 命令行选项
2. 用户配置文件 (`~/.ssh/config`)
3. 系统配置文件 (`/etc/ssh/ssh_config`)

配置文件可分为多个配置区段，每个配置区段使用 `Host` 来区分。我们可以在命令行中输入不同的 `Host` 来加载不同的配置段。对每一个配置项来说，首次获取的参数值将被采用，因此通用的设置应该放到文件的后面，特定 `Host` 相关的配置项应放到文件的前面。

例如 `~/.ssh/config` 文件加入如下配置：
```bash
# 快捷ssh登陆
Host mac #关键词
 HostName 192.168.1.166 #主机地址或者IP地址
 User XIN #用户名
```

命令行中输入 `ssh mac` 即可 `SSH` 快捷登陆:
```shell
➜  ~ ssh mac
Last login: Sun Jul 14 14:44:49 2019 from 192.168.1.158
➜  ~
```

## 配置项说明
**Host**

用于我们执行 SSH 命令的时候如何匹配到该配置。
* `*`， 匹配所有主机名
* `*.example.com`，匹配以 .example.com 结尾
* `!*.dialup.example.com,*.example.com`，以 ! 开头是排除的意思。
* `192.168.0.?`，匹配 192.168.0.[0-9] 的 IP。

当然我们也可以自定一个关键词，比如上述的 `mac`

**HostName**

指定远程主机名，可以直接使用数字IP地址。如果主机名中包 `%h` ，则实际使用时会被命令行中的主机名替换。

**GlobalKnownHostsFile**

指定一个或多个全局认证主机缓存文件，用来缓存通过认证的远程主机的密钥，多个文件用空格分隔。默认缓存文件为：
/etc/ssh/ssh_known_hosts,/etc/ssh/ssh_known_hosts2

**ControlPath**

指定 control socket 的路径，值可以直接指定也可以用一下参数代替：

* %L 本地主机名的第一个组件
* %l 本地主机名（包括域名）
* %h 远程主机名（命令行输入）
* %n 远程原始主机名
* %p 远程主机端口
* %r 远程登录用户名
* %u 本地 ssh 正在使用的用户名
* %i 本地 ssh 正在使用 uid
* %C 值为 %l%h%p%r 的 hash

**AddKeysToAgent**

是否自动将 key 加入到 `ssh-agent`，值可以为 no(default)/confirm/ask/yes。

如果是 yes，key 和密码都将读取文件并以加入到 agent ，就像 `ssh-add`。其他分别是询问、确认、不加入的意思。添加到 `ssh-agent` 意味着将私钥和密码交给它管理，让它来进行身份认证。

**IdentityFile**

指定读取的认证文件路径，允许 DSA，ECDSA，Ed25519 或 RSA。值可以直接指定也可以用一下参数代替：

* %d，本地用户目录 ~
* %u，本地用户
* %l，本地主机名
* %h，远程主机名
* %r，远程用户名

**Port**

指定连接远程主机的哪个端口，22(default)。

**ProxyCommand**

指定连接的服务器需要执行的命令。%h，%p，%r

例如：
```bash
ProxyCommand /usr/bin/nc -X connect -x 192.0.2.0:8080 %h %p
```

**User**

登录用户名


> 更多配置，可以终端输入 `man ssh_config 5` 查看。