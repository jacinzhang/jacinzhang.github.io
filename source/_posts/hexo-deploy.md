---
title: Hexo 博客搭建 
date: 2019-04-20 17:52:06
tags: hexo
categories: blog
---
周末闲暇之余，重新搭建了 blog，这里记录下，方便以后查阅。

所采用的是 `Hexo` + `GitHub Pages` + `Travis CI`。
具体涉及到以下几个方面。

# hexo 的安装
hexo 的安装，主要参考官方文档，[传送门](https://hexo.io/zh-cn/)
# theme 的选择
[主题](https://hexo.io/themes/)的选择，hexo 安装成功后，默认用的 landscape 主题，不太好看，这里我选择了[clean-blog](https://github.com/klugjo/hexo-theme-clean-blog)这一主题。
> 如果你的源码文件采用 git 版本控制，然后你的主题采用 `$ git clone https://github.com/klugjo/hexo-theme-clean-blog.git themes/clean-blog`clone的话，clone 完成后，需要进入 `themes/clean-blog`文件夹，删除主题的 `.git` 文件夹，将其加入源码工程的版本控制。

# 环境的配置
* `_config.yml`

git 部署配置
```yml
deploy:
  type: git
  repo: git@github.com:jacinzhang/jacinzhang.github.io.git
  branch: master
```
# travis ci 的集成
* [GitHub Person Access Token](https://github.com/settings/tokens) 配置
* [Travis CI](https://travis-ci.org/)的开启
* **.travis.yml**文件的编写

.travis.yml具体内容如下:
```yml
language: node_js
node_js: stable

notifications:
  slack: jacinzhang:6CR3iovkPBV5LFmW9bBnCsTl
  
branches:
  only:
    - hexo

# S: Build Lifecycle
install:
  - npm install
  - npm install -g hexo-cli 


#before_script:
 # - npm install -g gulp

script:
  - hexo clean
  - hexo generate

after_script:
  - cd ./public
  - git init
  - git config user.name "${USER_NAME}"
  - git config user.email "${EMAIL}"
  - git add .
  - git commit -m "Update docs"
  - git push --force --quiet "https://${GH_TOKEN}@${GH_REF}" master:master
# E: Build LifeCycle

env:
    global:
        - GH_REF: github.com/jacinzhang/jacinzhang.github.io.git
```
> `${GH_TOKEN}` 是刚生成的 **GitHub Person Access Token**，将其配置在 travis ci 的项目环境变量中
> `${USER_NAME}` git 提交时用户名，也配置在 travis ci 项目环境变量中
> `${EMAIL}` git 提交时邮箱，也配置在 travis ci 项目环境变量中
