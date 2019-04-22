---
title: 【Git 学习笔记】git 命令
date: 2019-04-22 14:49:59
tags: git
categories: 杂七杂八
---

* 推送所有本地分支到远程 
```bash
git push origin '*:*'
# or
git push origin --all
```

* 推送所有 tag 到远程
```bash
git push origin --tags
```

* 推送所有本地分支和tag到远程
```bash
git push origin --mirror
```

* 删除远程分支
```bash
git push --delete origin branch
```

* 分支详情信息(可查看本地分支track远程信息)
```bash
git branch -avv
```

* [当前分支正在 track 的远程分支](https://stackoverflow.com/questions/171550/find-out-which-remote-branch-a-local-branch-is-tracking)
```bash
git rev-parse --abbrev-ref --symbolic-full-name @{upstream}
```

* 移除已加入版本库的文件
```bash
git rm -r --cached .idea/
```

* 显示当前分支
```bash
git rev-parse --abbrev-ref HEAD
```

* 引用列表
```bash
# 远程
git ls-remote 
# 本地
git show-ref
```

* 远程仓库完整信息
```bash
git remote show origin
```

* 显示简短 commit id
```bash
git rev-parse --short HEAD
```

* 版本差异对比
```bash
git show <commit_id> #查看之前的提交记录
git diff #只能对比已加入版本控制的文件改动
git diff --cached #新增文件，可先 `git add --all`加入暂存区，再使用 --cache 参数查看改动内容
```

* 指定参数git clone 
```bash
git clone -b master --depth 1 git@github.com:AFNetworking/AFNetworking.git ZXYNetwork
```

* 深度拉取(针对 clone 时加了--depth 参数)
```bash
git pull --unshallow
```

* .gitignore 
```
/git_test/与 git_test/ 区别
/git_test/ 只会忽略与.gitignore同级目录下的 git_test 目录，
git_test/ 忽略所有的 git_test 目录。
```

---
> 上述 origin 为远程仓库的名字，如果不是以 origin 命名，需要改成相应的名字。