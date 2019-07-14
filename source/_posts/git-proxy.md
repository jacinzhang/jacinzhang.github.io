---
title: 【工具配置】Git 配置 Shadowsocks 代理
toc: true
date: 2019-07-14 16:42:16
tags: 
 - git
 - proxy
categories:
---

git `clone`仓库时有如下两种形式：
* HTTP 形式：
> git clone https://github.com/owner/git.git
* SSH 形式：
> git clone git@github.com:owner/git.git

对天朝用户来说，使用上述的任意方式 `clone` github 上的仓库时，速度都可能很慢，所以就有了 git 代理的出现...

上述两种 `clone` 方式代理方式是不同的，下面分别做介绍。

# HTTP 形式
HTTP 形式的 `clone` 方式有如下两种代理方式设置：

## HTTP 代理
通过 http 链接 clone 代码时走 http 代理
```bash
git config --global http.proxy "http://127.0.0.1:1087"
git config --global https.proxy "http://127.0.0.1:1087"
```
> 端口 `1087` 需要在 Shadowsocks 设置里面确认，如下图所示：

![img](https://user-images.githubusercontent.com/9859965/61181942-74037b80-a65f-11e9-8ddf-bdb3d1bb92cc.png)

## socks5 代理
通过 http 链接 clone 代码时走 socks5 代理
```bash
git config --global http.proxy "socks5://127.0.0.1:1080"
git config --global https.proxy "socks5://127.0.0.1:1080"
```
> 端口 `1080` 需要在 Shadowsocks 设置里面确认，如下图所示：

![img](https://user-images.githubusercontent.com/9859965/61181953-9ac1b200-a65f-11e9-9f66-5316200c13d3.png)

设置完成后，这些配置都可以在 `~/.gitconfig` 下看到：

```bash
# HTTP 代理
[http]
	proxy = http://127.0.0.1:1087
[https]
	proxy = http://127.0.0.1:1087
```
或者
```bash
# socks5 代理
[http]
	proxy = socks5://127.0.0.1:1086
[https]
	proxy = socks5://127.0.0.1:1086
```

# SSH 形式
还有一种情况，我们通过 `SSH` 方法 `clone` 代码，提交代码，因为这样不用输入密码，通常我们会在自己的常用电脑上这么做。***上面设置的 `HTTP` 代理对这种方式 `clone` 代码是没有影响的，也就是并不会加速***，`SSH` 的代理需要单独设置，其实这个跟 `Git` 的关系已经不是很大，我们需要改的，是 `SSH` 的配置。在用户目录下建立如下文件 `~/.ssh/config`，对 GitHub 的域名做单独的处理。


```bash
Host github.com
 HostName github.com
 User git
 # 如果是 HTTP 代理，把下面这行取消注释，并把 proxyport 改成自己的 http 代理的端口
#  ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=1087
 # 如果是 socks5 代理，则把下面这行取消注释，并把 1086 改成自己 socks5 代理的端口
  ProxyCommand nc -v -x 127.0.0.1:1086 %h %p
```

# 代理后效果
下面感受下代理前后的 `clone` 效果：

未代理时：
![before](https://user-images.githubusercontent.com/9859965/61181968-c93f8d00-a65f-11e9-895c-0efd9eef5d95.png)

socks5 代理后：
![after](https://user-images.githubusercontent.com/9859965/61181959-b0cf7280-a65f-11e9-80ed-c976ddf3da0d.png)