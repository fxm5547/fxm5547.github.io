---
layout:     post
title:      "Git使用指导"
subtitle:   "基于Coding代码托管的Git基本使用指导"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
    - 工具手册
tags:
    - Git
    - 使用手册
---


*适合：开发和测试人员*

## 参考
**必读：**<https://coding.net/help/doc/git/getting-started.html>
[Git常用命令速查表](https://dn-coding-net-production-pp.qbox.me/e8dd7837-b39d-413e-9beb-ed51984719e0.png)
[廖雪峰的Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
[git教程中文版v2](https://git-scm.com/book/zh/v2)

## 安装Git客户端
[安装Git](https://git-scm.com/downloads)
[安装图形化工具Sourcetree](https://www.sourcetreeapp.com)

## 命令行示例

#### 添加远程仓库

对当前工程开始用 Git 管理，只需到所在的目录，执行：
`$ git init`

添加远程仓库：
`$ git remote add origin https://git.coding.net/fxm5547/gitest.git`

接下来用 git remote 命令来查看当前添加的远程仓库：
`$ git remote -v`

#### 或克隆远程仓库
- 没有submodule时：`$ git clone https://git.coding.net/fxm5547/gitest.git`
- 有submodule时：`$ git clone --recursive https://git.coding.net/fxm5547/gitest.git && cd gitest && git submodule foreach git checkout master`

#### 添加submodule
`$ git submodule add https://git.coding.net/fxm5547/submodule-name.git submodule-dir`
这样在`submodule-dir`目录下就是`submodule-name`的代码，根目录会增加一个`.gitmodules`的配置文件。

#### 永久保存用户名和密码
`$ git config credential.helper store`

#### 分支
新建分支：
`$ git branch develop`

切换到develop分支：
`$ git checkout develop`

分支推送到远程仓库 git push [仓库名] [分支名]：
`$ git push origin develop`


#### 更新代码
- 没有submodule时：
  - `$ git pull`
  - **100%更新代码成功（忽略一切本地更改）：**`git fetch --all && git reset --hard origin/master && git checkout master`
- 有submodule时：
  - `$ git pull && git submodule foreach git pull`
  - **100%更新代码成功（忽略一切本地更改）：**`git fetch --all && git reset --hard origin/master && git checkout master && git submodule foreach git fetch --all && git submodule foreach git reset --hard origin/master && git submodule foreach git checkout master `


#### 提交代码
查看当前工作目录的文件状态：
`$ git status`

将修改／新增的文件放入暂存区：
`$ git add login.code`

提交至本地仓库：
`$ git commit login.code -m "完成登录功能"`

推送到远程仓库git push [远程仓库名] [分支名]：
`$ git push origin develop`

```
$ touch login.code & echo 'login'>login.code
$ git add login.code
$ git commit login.code -m "完成登录功能"
```

#### 合并分支
**目前用不到，一律通过Coding控制台新建MergeRequest合并到Master**

本地仓库更新到最新，每次合并前都这么做git pull [远程仓库名] [分支名]:
`$ git pull origin develop`

将指定分支合并到当前工作分支git merge [分支名] :
`$ git merge develop`

```
$ touch reg.code & echo 'register'>reg.code
$ git add reg.code
$ git commit reg.code -m "完成注册功能"
$ git checkout master
$ git pull 
$ git merge develop
```

merge时出现冲突，手动解决之后add和commit即可

#### Merge Request

[参考](https://coding.net/help/doc/git/git-branch.html#section-8)
在Coding控制台操作，项目负责人授权或直接合并即可。

#### git reset

还原到commit ID 指定的版本：
`git reset --hard HEAD~3`

#### git revert

还原到提交前的版本


#### 发布管理

- 发布新版流程：
  - 在Coding控制台删除旧的 release branch，并从当前的 master 创建新的 release branch；
  - 服务器更新代码：
```
$ git fetch --all && git reset --hard origin/release && git checkout release && git submodule foreach git fetch --all && git submodule foreach git reset --hard origin/release && git submodule foreach git checkout release
```
  - 在Coding控制台基于当前release分支新建tag。

- Bugfix 流程： bugfix 指的是修复已经发布的程序（release branch）中的缺陷。
  - 在本地release branch 从 master cherrypick 修复该缺陷的一个或多个 commit；
```
$ git checkout release
$ git pull
$ git cherry-pick 2163f0331bb2d5491cf84fe4d5a0d638ed92afb1
$ git push origin release
```
*cherry-pick的commit-hash可通过 `git log` 或在控制台查看*
- 服务器更新代码：
```
$ git fetch --all && git reset --hard origin/release && git checkout release && git submodule foreach git fetch --all && git submodule foreach git reset --hard origin/release && git submodule foreach git checkout release
```
  - 在Coding控制台基于当前release分支新建tag。


## JetBrain IDE中使用Git

#### 使用内置的控制台
 ![图片](https://dn-coding-net-production-pp.qbox.me/9c7d3679-6731-45b6-b126-f2bcbf0a39dd.png) 

#### 使用图形化插件
切换/新建分支
 ![图片](https://dn-coding-net-production-pp.qbox.me/6b41a1ba-e6cb-4f76-9d32-9fe5bbfe69be.png) 
常用的操作
 ![图片](https://dn-coding-net-production-pp.qbox.me/a7f96754-9493-429a-92a1-7310d3fb4a37.png?imageView2/0/w/500)

#### 使用快捷键
开始编码前Update Project工程，将所有分支更新到最新：
 ![图片](https://dn-coding-net-production-pp.qbox.me/1149fde9-e18a-4915-aa22-c022efb5d0f1.png) 

## 注意事项
- Git对于空目录默认不进行版本控制，请通过添加.gitkeep空文件使其被track
- 通过.gitignore添加不需要版本控制的文件
- 执行以下命令解决大文件传输问题`git config --global http.postBuffer 1048576000`