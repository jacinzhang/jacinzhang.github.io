---
title: 【Python 学习笔记】pyenv 管理 python 版本
toc: true
date: 2019-04-20 19:03:11
tags: 
    - python
    - pyenv
    - virtualenv
categories: python
---
# 安装配置 (for macOS users)
1. [pyenv](https://github.com/pyenv/pyenv)
```bash
brew install pyenv
```
2. [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)
```bash
brew install pyenv-virtualenv
```

`pyenv` 和 `pyenv-virtualenv` 都安装成功后，在 
```bash
~/.zshrc #iTerm用户
~/.bash_profile #Terminal用户
```
中添加如下初始化命令
```bash
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

# pyenv 使用
```bash
# 列举所有可安装版本
pyenv install --list
# 安装 3.7.2 版本
pyenv install 3.7.2
# 当前目录下设置为 3.7.2 版本
pyenv local 3.7.2
# 列举所有版本(包含系统版本)
pyenv versions
```

# pyenv-virtualenv 使用
```bash
# 创建 3.7.2 的虚拟环境版
pyenv virtualenv 3.7.2 env-3.7.2
# 创建当前版本的虚拟环境
pyenv virtualenv venv34
# 激活虚拟
pyenv activate <name>
# 失活虚拟环境
pyenv deactivate
# 移除虚拟环境
pyenv uninstall my-virtual-env
```