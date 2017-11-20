---
layout:     post
title:      "Linux/Mac配置常用alias"
subtitle:   "配置alias提升效率"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-2015.jpg"
catalog: true
categories:
    - 工具手册
tags:
    - alias
    - Linux
---

#  常用alias及配置指导
#### 现有常用
- 简单版拉最新代码: `alias gp='git clean -fd && git stash && git pull'`
- 快速进入dev目录:  `alias dev='cd /apps'`
- 强力版拉最新代码: `alias gfp='git fetch --all && git reset --hard origin/master && git checkout master && git submodule foreach git fetch --all && git submodule foreach git reset --hard origin/master && git submodule foreach git checkout master'`

#### 如何配置（非常简单）
- 默认终端：`vim ~/.bashrc`
- Oh My Zsh：`vim ~/.zshrc`
- 所有用户生效：`vim /etc/profile`

- `source ~/.bashrc`或重新进入终端后生效。