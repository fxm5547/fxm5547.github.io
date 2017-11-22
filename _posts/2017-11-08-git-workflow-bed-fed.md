---
layout:     post
title:      "Git工作流及发布规范（BED-FED）"
subtitle:   "后端开发和Web前端开发Git工作流及发布规范"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
    - 研发流程
tags:
    - Git
    - 工作流
---

## 参考

- <http://open.leancloud.cn/git-branch-guide.html>
- <https://blog.coding.net/blog/feature-branch-workflow>
- <https://blog.coding.net/blog/git-workflow>
- <https://blog.coding.net/blog/principle-of-Git>


## 介绍

本约束规则适用于孩宝所有后端和前端工程代码。管理工具使用[Coding.net](https://coding.net/user)提供的git托管服务。

Git的workflow有多种，各有利弊，无所谓好坏。但团队协作需要有一致的规范，所以请大家务必遵守。

除了一致性之外，这个规范的目的是以下几点：
- 方便开发和测试同学协同，高效完成研发工作，产出高质量的成果。
- 确保可以轻易确定特定时间发布或运行的版本。在新发布的程序存在重大缺陷时，可以尽快 rollback 到上一个稳定版本。
- 在需要修复紧急 bug 并尽快发布时，可以只发布必要的 bugfix 而不同时发布还不应发布的其他改动。


## branch和tag

**使用Feature Branch Workflow，按照需求新建feature branch**

Branch: **feature branch**、**master** 和 **release**。master是默认分支，release 是用于发布的分支。

   - **feature branch:** 功能开发或bug修复从master新建一个分支，push到远程仓库，提交合并至master的请求，合并后删除该分支；需要多人协作的功能开发，负责人新建分支，共同在该分支上开发，可以测试时提交合并至master的请求，功能上线后删除该分支。
   - **master:** 只负责合并各feature branch的代码，且保证master分支随时处于可测试，测试之后可发布状态。 *提交后自动部署到测试环境*。
   - **release:** 是当前发布的分支，在这个分支只能从master新建 或 增加从 master cherrypick 过来的 commit。
  
Tag: 对应每个发布版本的 tag。

- SDK 和App应用程序的 tag 遵照 `<major>.<minor>.<patch> `的命名，如 2.5.1，参考[SemVer](http://semver.org/)；
- 服务端程序的 tag 以发布的日期命名，如 2016.07.28，如果有 bugfix，则在后面增加小写字母，如 2016.07.28 后是 2016.07.28a，然后是 2016.07.28b。
 ![图片](https://dn-coding-net-production-pp.qbox.me/9d8c5e1a-b5f5-4fcc-a647-98aab350daef.png) 
[branch&tag](https://www.processon.com/view/link/5989831ae4b02783dc348959)

**代码提交应尽量采用原子性的提交，即基于单一功能的提交（worktile单一任务或其拆分出的功能），不建议一次性提交多个功能，必须保证每次提交都是可执行的完整功能。提交时必须写清晰的提交日志。**


## 开发测试流程
- 开发测试流程
![图片](https://dn-coding-net-production-pp.qbox.me/dd3a8458-0339-437d-8534-486b1a04119b.png) 
[开发/测试/部署流程](https://www.processon.com/view/link/598982b7e4b0d7c12dfcfd40)
- 搭建统一的本地开发测试环境，推荐[Vagrant](https://www.vagrantup.com)：

## 发布管理

**所有版本发布前，测试工程师必须确认测试已完全覆盖并通过。** 

- 发布新版流程：删除旧的 release branch，并从当前的 master 创建新的 release branch；
- Bugfix 流程： bugfix 指的是修复已经发布的程序（release branch）中的缺陷。在 release branch 从 master branch cherry pick 修复该缺陷的一个或多个 commit；

### 发布新版本详细步骤
1.    Coding上删除release分支
2.    Coding上从master分支新建release
3.    在服务器上执行发布新版本的脚本

### 发布补丁详细步骤
1.    先update整个工程
2.    git切换到release分支
3.    执行git status命令
4.    执行 git cherry-pick commit_id 命令
5.    如果遇到冲突，解决冲突，解决冲突的办法是接受他们的代码，解决冲突后commit file && push file，如没遇冲突则直接push file
6.    进入coding查看release分支的代码是否有被更新，代码已更新则继续下面步骤，没有被更新则查找原因
7.    执行发版脚本
8.    通知对应的开发人员以及测试人员进行生产验证
9.    进入coding打上标签，标签命名为日期加上a-z的小写字母


## 其他

- 并不是每个 bug 都有专门发布 bugfix 版的必要，对于不紧急的 bug，可以 fix 后随下一个版本发布。
- master分支只有负责人有readwrite权限，其他开发人员只有read权限。release分支只有负责发版的人员有readwrite权限。