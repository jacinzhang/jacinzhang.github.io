---
title: 【Python 学习笔记】基本概念
toc: true
date: 2019-04-21 15:28:26
tags: python
categories: python
---
# 基本名词概念

## Shebang
在脚本语言中, 第一行以 `#!` 开头的代码, 在计算机行业中叫做[Shebang](https://zh.wikipedia.org/wiki/Shebang)，其作用是**指定由哪个解释器来执行脚本**。
格式：`#!/path/to/script/interpreter`
例如:
```bash
#!/bin/sh           shell脚本
#!/usr/bin/perl     perl脚本
#!/usr/bin/python   python脚本
#!/usr/bin/python3  python3脚本
#!/usr/bin/python2  python2脚本
```

而有时不太清楚脚本解释器的具体全路径，或者开发环境与运行环境的安装路径不同。为了保证兼容性，也可以写作如下格式：

```bash
#!/usr/bin/env python3
```
> 大部分 Python 文件不必写 Shebang, 只有被直接执行的文件才有必要加入 Shebang。

## python 文件编码

```bash
# -*- coding: utf-8 -*-
```
此行注释是为了告诉 Python 解释器，按照 UTF-8 编码读取源代码。
## 模块

在 python 中，一个 `.py` 文件就称之为一个模块(Module)。 