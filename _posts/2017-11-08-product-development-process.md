---
layout:     post
title:      "产品研发流程"
subtitle:   "产品研发团队基于Worktile的Scrum敏捷开发协作流程"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 研发流程
    - 项目管理
tags:
    - 产品研发流程
    - Scrum敏捷开发
---

*最佳实践，适用于整个产品研发团队，参考：[Scrum中文网知识库](http://www.scrumcn.com/agile/scrum-knowledge-library/scrum.html)*

## 产品研发完整流程

 ![图片](https://dn-coding-net-production-pp.qbox.me/e2a75e1c-0320-413d-b483-9bda7da083ac.png) 
[产品研发流程](https://www.processon.com/view/link/598982cde4b0e56e5d085eb4)

## 准则
- 大的版本，按模块进行，把Product Backlog拆成多个Sprint Backlog进行；
- **产品超前设计1-2个Sprint**，设计包括：UI设计、开发设计、测试用例设计；
- **设计超前后端开发1-2个Sprint**；
- **后端开发超前前端开发1-2个Sprint**；
- **所有需求，必须先经过需求确定阶段，不允许直接提给开发同学；生产环境问题是bug不是需求，提给QA同学**；
- **产品输出必须详尽，Sprint计划会议后不允许修改需求**。

## 角色
- 产品负责人
- Scrum Master
- 产品团队：产品和设计同学
- 研发团队：开发和测试同学


## 产品Worktile协作流程
 ![图片](https://dn-coding-net-production-pp.qbox.me/b37f8fbf-848c-4cff-b70f-f559e4c8273e.png) 
[产品Worktile协作流程](https://www.processon.com/view/link/598982e9e4b0d7c12dfcfd77)

## 研发Worktile协作流程（BED & FED）
![图片](https://dn-coding-net-production-pp.qbox.me/98b7c35a-1a7c-4762-b180-28691cc71dda.png) 
[研发Worktile协作流程（BED & FED）](https://www.processon.com/view/link/5989827de4b058e0a2f1b831)

## 研发Worktile协作流程（APP）
 ![图片](https://dn-coding-net-production-pp.qbox.me/9ecee02b-a7ca-4a9f-b614-c27d610dcb4e.png) 
[研发Worktile协作流程（APP）](https://www.processon.com/view/link/59898290e4b02783dc3488e0)

## 研发会议安排
#### Sprint计划会议
- 每个Sprint都以Sprint计划会议作为开始；
- **目的：** Scrum团队共同选择和理解在即将到来的Sprint中要完成的工作；
- **周期：** Sprint周期一般为1周，特殊情况不超过2周；
- **时长：** Sprint计划周数 * 2小时内；
- **成员：** 整个团队；
- **职责：** Sprint Backlog的需求及优先级来至产品负责人，对Sprint Backlog任务的安排、拆解、细化由Scrum Master完成；
- **标记：** Sprint任务设置截止日期，**Scrum Master心中要有数：产品同学当前Sprint的任务是设计同学之后1-2个Sprint迭代应该承接的任务；设计同学当前Sprint的任务是后端开发同学之后1-2个Sprint迭代应该承接的任务；后端开发同学当前Sprint的任务是前端开发同学之后1-2个Sprint迭代应该承接的任务；测试同学当前Sprint的任务应该在该Sprint结束前发布**。

- **Sprint原则**
   - Sprint任务优先，如需插入新的紧急任务需要与Scrum团队协商（生产环境问题除外）；
   - Scrum Master需要分清楚优先级，并协调好开发任务；
   - Scrum团队需要齐心协力；
   - Scrum团队需要提前准备Scrum会议内容；
   - Scrum Master是Scrum团队一起的，并不是独立出去的角色；
   - Scrum团队成员平等、齐心、自由。

#### 每日Scrum会议
- 每日Scrum会议来确认每日要完成的Sprint待办事项；
- **目的：** 确认我们仍然可以实现Sprint的目标，交流进展和需要协作的问题；
- **周期：** 每天；
- **时长：** 每次不超过15分钟；
- **成员：** 整个团队；
- **周期：** 每天；
- 团队成员依次快速描述自己昨天完成了哪些Sprint待办事项、今天准备做哪些待办事项、有哪些Sprint待办事项需要其他团队成员协调。

#### Sprint回顾会议
- **目的：** 回顾一下团队在流程、人际关系以及工具方面做得如何，讨论并得出改进措施运用于下一个Sprint；
- **时长：** Sprint计划周数 * 1小时内；
- **成员：** 整个团队；
- **周期：** Scrum Master发现可能存在问题时开，如进展顺利可与下一次Sprint计划一起开。

#### 技术方案评审会议
- **目的：** 评审技术方案以期获得最好的方案，并给团队介绍方案；
- **时长：** 视具体方案；
- **成员：** 相关开发同学；
- **周期：** 技术方案实施前。

#### 测试用例评审会议
- **目的：** 评审测试用例，保证准确率和覆盖率；
- **时长：** 视具体产品而定；
- **成员：** 产品和开发同学；
- **周期：** 测试开始前。

## 文档协作

#### 需求文档 
  - 在石墨上文档相应文件夹内，可多人实时编辑，秒级同步；
  ![图片](https://dn-coding-net-production-pp.qbox.me/c90928be-a548-48ac-beef-3441b0bdeb63.png) 

 - 在部门共享盘里新建文档放置石墨文档的链接：
 ![图片](https://dn-coding-net-production-pp.qbox.me/9074a44b-c982-423d-a68f-beb883fa0f59.png) 
 ![图片](https://dn-coding-net-production-pp.qbox.me/efa65880-eb1e-4ee8-90e5-df8a1e9a6170.png) 

#### 图表
- 包括：产品结构图、产品用例图、产品业务逻辑图、测试用例思维导图、业务实现逻辑图；
- 在ProcessOn的对应小组内；
 ![图片](https://dn-coding-net-production-pp.qbox.me/fde07f48-a189-40d1-b0bc-4faf3a695867.png) 
- 用于：需求文档内、实现相关文档、任务说明等；
- 对于用于描述功能实现的图，在部门共享盘里新建文档放置图的链接：
 ![图片](https://dn-coding-net-production-pp.qbox.me/fce74f5a-a636-4718-a4c4-b6c46c2de209.png) 
 ![图片](https://dn-coding-net-production-pp.qbox.me/0af653e8-4acb-46dd-9071-fc0e2df072d3.png)


## 配合环节输出的具体要求
#### 业务部门—>产品
- **需求说明**
  - 格式：Worktile任务
  - 提至：**App bug与需求收集** 和 **站bug与需求收集** 项目的**功能改进**、**新增需求**、**运营需求**任务列表列表
 ![图片](https://dn-coding-net-production-pp.qbox.me/b5719aa7-e548-4aae-a9e4-6a8e62d561b3.png) 
  - 要求：描述清楚需求的目标用户、使用场景等；
  - 模板：如何将新增需求描述清楚
    - 这个需求的目标用户有那些？
    - 这个需求解决了什么问题，解决之后达到怎样的效果？
    - 这个需求主要使用的场景是什么？
    - 是否有其他参考方案或竞品？
    - 未来三个月内，针对该需求实现后，我们的运营计划是什么？
  
- **活动策划方案**
  - 格式：文档
  - 提至：需求说明附件
  - 要求：
  - 模板：

#### 产品—>设计、开发、测试
- **原型Mockup**
  - 格式：墨刀、Axure原型
  - 提至：任务说明
  - 要求：
    - 仅交付设计师一份完整的原型图；
    - 原型图要详尽，每个功能点在原型上都有对应的标注；
    - 原型图以实例呈现需求；
    - 原型图标注尽可能精炼，不允许有概念模糊的文案或功能名称出现；
    - 原型图不必填充图片，以黑白灰深浅色的方法表现层级关系即可；
    - 设计师在交互上的变更产品需提前/同步修改原型/文档；
    - 最后保证原型图与QA验收的需求文档一致
  - 模板：
- **产品需求文档PRD**
  - 格式：石墨文档
  - 提至：任务说明
  - 要求：
    - 保持和视觉设计图一致；
    - 包括产品结构图、产品用例图、产品业务逻辑图等；
    -  需求说明需做到完备，尽量涵盖正常状态、数据缺失、服务异常等实际开发和使用过程中可能产生的各种情况。
  - 模板：

#### 设计—>开发
- **视觉设计图和标注**
  - 格式：Zeplin
  - 提至：任务说明
  - 要求：
    - 保持和PRD文档一致；
    -  使用评论功能来尽量明确设计意图，以及需要开发同学注意的地方：比如底部留白等；
    -  使用拉线标注等方法，明确页面中需要开发设置的元素，避免页面中元素过多时，开发时遗漏；
    -  动画等动态交互需要提供具体、可复现、可操作的参数；
    - 设计评审之后，本地共享盘放置一份jpg效果图。
  - 模板：
- **交互说明**
  - 格式：PRD
  - 提至：任务说明
  - 要求：
    - 必要的标注；
  - 模板：

#### 开发—>测试
- **技术实现方案**
  - 格式：文档（逻辑流程、技术实现流程、存储方案等为主）
  - 提至：任务说明
  - 要求：简洁解释
  - 模板：
- **接口文档**
  - 格式：apiDoc在线文档
  - 提至：任务说明
  - 要求：
    - [apiDoc定义规范]({% post_url 2017-11-08-apiDoc-define-standard %})
    - [RESTful API定义及使用规范]({% post_url 2017-11-08-RESTful-API-standard %}) 
  - 模板：https://api.baobaobooks.net/docs/account/
- **版本更新日志**
  - 格式：文档
  - 提至：任务说明
  - 要求：清晰描述此版本修改的模块，已经可能涉及到的模块。
  - 模板：

#### 测试—>产品、开发
- **测试帐户和仿真测试数据**
  - 提至：联系获取
  - 要求：
  - 模板：

#### 测试—>项目经理
- **测试报告/可发布评估报告**
  - 格式：文档（数据为主）
  - 提至：Worktile项目的“发版备忘”列表
  - 要求：简明清晰
  - 模板：