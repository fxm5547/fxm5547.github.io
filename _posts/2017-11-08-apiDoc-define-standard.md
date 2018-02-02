---
layout:     post
title:      "apiDoc定义规范"
subtitle:   "使用apiDoc书写API文档规范"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
tags:
    - apiDoc
    - API
    - 接口文档
    - BED
---

 
### 详细阅读apiDoc官方文档
- 详细阅读官方文档：<http://apidocjs.com>


### 项目中apiDoc文件结构
- 整体结构
 ![图片](https://dn-coding-net-production-pp.qbox.me/40f4702d-0b3c-4c6e-8583-cefb5e7f9bec.png) 

- `apidoc.json`
 ![图片](https://dn-coding-net-production-pp.qbox.me/52ccda25-2657-4941-827f-9880abd70947.png) 

- `common.php`
  - 公共部分定义-权限（apiPermission）
    - 定义
 ![图片](https://dn-coding-net-production-pp.qbox.me/04618725-457e-417d-a428-68735221080c.png) 
    - 使用
     ![图片](https://dn-coding-net-production-pp.qbox.me/0c8ad25f-2168-42b6-bc12-af039750f659.png) 
  - 公共部分定义-状态码分组（apiSuccess、apiError）
    - 定义
 ![图片](https://dn-coding-net-production-pp.qbox.me/63afaa67-2759-42ec-a9b0-fe5b8a43ecb9.png) 
    - 使用
 ![图片](https://dn-coding-net-production-pp.qbox.me/a4bccc4f-5d1a-4975-8fe1-06059d5cb20d.png) 
 ![图片](https://dn-coding-net-production-pp.qbox.me/b25cbacf-1190-48d8-8adc-bb41762c122e.png) 
  - 公共部分定义-错误响应（apiError、apiErrorExample）
    - 定义
 ![图片](https://dn-coding-net-production-pp.qbox.me/931d2e77-a353-4efa-8ecb-b4e763be8a04.png) 
    - 使用
 ![图片](https://dn-coding-net-production-pp.qbox.me/e56365d6-5900-4561-92ff-ea270405daa6.png) 

- `define.php`
  -  公共部分定义-api分组
    - 定义
 ![图片](https://dn-coding-net-production-pp.qbox.me/ccedc23a-9648-4e08-b56d-084f24c4454b.png) 
    - 使用
 ![图片](https://dn-coding-net-production-pp.qbox.me/5c49a0c8-cb2d-44de-b053-f4dc6ed36c01.png) 


### 接口具体apidoc定义
- 接口最新定义在代码实现处，历史版本定义在apidoc/history.php中。
- 接口定义完整示例：
 ![图片](https://dn-coding-net-production-pp.qbox.me/4256566c-53e0-42c7-9d62-22bf4a9d03bf.png) 

-  `@apiVersion`
  - 目前只用到major和minor，patch始终为0。

- `@apiName`
  - 从`@api`定义转换而来：
   如`@api`为：`@api {put} /user/babies/:baby_id 修改宝宝信息`，
  则`@apiName`为: `@apiName put/user/babies/:baby_id`，
  则解析后的ID为；`put_user_babies__baby_id`（用于apidoc.json的order接口排序）。

- `@apiGroup`
  - 接口分组，定义在`apidoc/define.php`，如`@apiGroup babyGroup`。

- `@apiPermission`
  - 接口权限，定义在`apidoc/common.php`，权限分为：
    - `none`：无需任何授权；
    - `token`：需要用户登录授权，可通过`header Authorization`和`Cookie HBSID`传递；
    - `admintoken`：需要管理员登录授权，可通过`header Authorization`和`Cookie HBCPSID`传递；
    - `token || admintoken`：用户登录授权或管理员登录授权都可以；
 ![图片](https://dn-coding-net-production-pp.qbox.me/77264ae7-c1a2-4d35-98a5-a57b61c4046e.png) 
    - `sign`：需要签名，一般用于服务端相互调用，详见[ API HMAC-SHA1签名](https://hbtown.worktile.com/drive/58f07f338341595437be627f/58f07f338341595437be62a9)。

- `@apiDescription`
  - 尽可能详细说明接口的用途及相关逻辑，如
  `@apiDescription 使用手机号找回密码的第一步，调用该接口先验证用户输入的手机号是否已经绑定某个帐号，未绑定给出提示，已经绑定则发送验证码、重置密码`。

- `@apiParam`
  - 准确定义数据类型；
  - 准确定义取值范围，如`{String{1..32}}`、`{String{YYYY-mm-dd}}`、`{String="0","1"}`；
  - 准确定义是否是可选参数，可选参数带`[]`，如`@apiParam {String} [stage]`；

- `@apiError`
  - 公共错误，直接使用`apidoc/common.php`中定义的错误，如`@apiUse InvalidToken`；
  - `NotFound`和`ValidationError`不允许使用公共定义错误（即不可使用`@apiUse`），需要准确定义具体错误，如:
 ![图片](https://dn-coding-net-production-pp.qbox.me/3fc05175-2708-427d-ac62-a6d4d5cea332.png) 

- `@apiSampleRequest`
  - GET接口：不写，默认使用`apidoc.json`的`sampleUrl`自动组装请求地址
  - 其他接口：`@apiSampleRequest off`，我们用Postman


### 接口分组
- 一般按功能模块分组，一个分组对应一个或多个php文件，每个php文件只对应一个分组；
- 所有权限为`admintoken`的接口（不包括权限为`token || admintoken`的接口），放在该接口模块的**管理中心接口**分组，`admin.php`文件中；
- 所有权限为`sign`的接口（短信模块除外），放在该接口模块的**内部服务接口**分组，`internal.php`文件中；


### 接口版本管理
- 同一个大版本下，只有当你的接口变更会影响到调用者时，才需要升级minor版本（如果被修改的版本还没有调用者，自然无需升级版本），如从1.0.0升至1.1.0。

- 升级版本时，需要将旧的apidoc注释拷贝至`apidoc/history.php`，并升级`apiVersion`
 ![图片](https://dn-coding-net-production-pp.qbox.me/2cb483b4-6c30-4a47-8eae-dd0df6415845.png) 

- 升级接口大版本时，拷贝旧版本文件目录作为新版本并升级接口版本（如拷贝v1，重命名为v2，修改新版本中所有接口为`2.0.0`版本）。

- 调用者在查看文档时，通过版本比较，可以轻易知晓新版本做了哪些变更。
 ![图片](https://dn-coding-net-production-pp.qbox.me/47958c75-6368-4034-8779-5c91b8317169.png) 
 ![图片](https://dn-coding-net-production-pp.qbox.me/3f1e483e-d9d0-4ff6-adc6-7e238c08f8bb.png) 

- 过期的接口，标记`@apiDeprecated`，说明应该使用哪些接口替代：
  - 在过期接口apidoc注释前增加：
 ![图片](https://dn-coding-net-production-pp.qbox.me/e078b65e-f246-4b1b-8777-ada84b4b6844.png) 
  - 文档显示：
 ![图片](https://dn-coding-net-production-pp.qbox.me/2671d908-fbcb-4f39-8042-1b1812941b0d.png) 


### 文档生成
- DEVQA服务器配置了定时任务(`crontab -l`查看)，每隔1分钟重新生成文档。
 ![图片](https://dn-coding-net-production-pp.qbox.me/5bf5d8c4-1d33-447c-9ae3-c2b7ed073ef9.png) 

- 新建接口模块时，
  - 需要修改定时任务`crontab -e`；
  - 在apidoc模板中新增导航`vim /usr/lib/node_modules/apidoc/template/index.html`；
 ![图片](https://dn-coding-net-production-pp.qbox.me/16ba3ef9-41e8-4c23-9992-0ad38b28dc10.png)


### api测试注意要点
- 是否严格遵循本规范定义接口；
- 错误处理周全，不遗漏任何的错误，错误的message必须简洁明了并给予指引，如“开团时间为1-5天，请重新输入”；
- 接口权限控制是否OK，是否存在安全隐患；
- 接口文档和实现是否完全一致；
-请求参数的名称、类型、是否可选、描述都必须准确和见名知意；
- 返回参数的名称、类型、描述都必须准确详尽。

### 修改后的多模块模板
[点击下载apidoc-template.zip]({{ site.baseurl }}/file/apidoc-template.zip)