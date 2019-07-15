---
title: 【Python 学习笔记】pip用法
date: 2019-04-22 23:53:26
tags: 
    - python
    - pip
categories: python
---
# pip 子命令
Python 有两个著名的包管理工具 `easy_install` 和 `pip`。`pip` 是 Python 包管理工具，该工具提供了对 Python 包的查找、下载、安装、卸载的功能。

|子命令	|解释说明|
|---|:---|
|install|	安装软件包|
|download|	下载软件包|
|uninstall|	卸载软件包|
|freeze|	按照requirements格式输出安装包，可以到其他服务器上执行pip install -r requirements.txt 直接安装软件|
|list|	列出当前系统的安装包|
|show|	查看安装包的信息，包括版本、依赖、许可证、作者、主页等信息|
|check|	检查安装包的依赖是否完整|
|config|	管理本地或全局配置文件|
|search|	查找安装包|
|wheel|	打包软件到wheel格式|
|completion|	生成命令补全配置|
|help|	获取pip和子命令的帮助信息|

下面以Flask为例，来看一下pip几个常用的子命令

```bash
# 查找安装包：
pip search flask

# 安装特定的安装包版本：
pip install flask==0.8

# 删除安装包
pip uninstall flask

# 查看安装包的信息：
pip show flask

# 检查安装包的依赖是否完整：
pip check flask

# 查看已安装的安装包列表：
pip list

# 导出系统已安装的安装包列表到requirements文件
pip freeze > requirements.txt

# 从requirements文件安装：
pip install -r requirements.txt

# 查看本地或全局配置：
pip config list

# 查看、修改、删除本地或全局配置：
pip config set 'global.index-url' 'https://pypi.douban.com/simple/'
pip config get 'global.index-url' 
pip config unset 'global.index-url'

# 使用pip命令补全：
pip completion --bash >> ~/.profile
source ~/.profile
```

使用豆瓣或阿里云的源加速软件安装
```bash
# 通过pip命令的-i选项指定镜像源即可，如下所示：
pip install -i https://pypi.douban.com/simple/ flask

# 每次都要指定镜像源的地址比较麻烦，可以修改Pip配置文件，将镜像源写入配置文件中。
# 豆瓣源，可以换成其他的源
pip config set 'global.index-url' 'https://pypi.douban.com/simple/'
# 添加豆瓣源为可信主机，要不然可能报错
pip config set 'trusted-host' 'pypi.douban.com'
# 取消pip版本检查，排除每次都报最新的pip
pip config set 'disable-pip-version-check' 'true'
# 设置超时时间
pip config set 'timeout' '120'
```

> 注：pip源配置文件可以放置的位置：
> /etc/pip.conf
> ~/.pip/pip.conf
> ~/.config/pip/pip.conf(使用pip config set命令时会创建在此目录中)

将软件下载到本地部署
```bash
# 下载到本地
pip download -d 'pwd' -r requirements.txt 

# 本地安装
pip install --no-index -f file://'pwd' -r requirements.txt
```