---
layout:     post
title:      "RESTful API规范"
subtitle:   " \"RESTful API定义及使用规范\""
date:       2017-08-17 18:42:02
author:     "fxm5547"
header-img: "img/post-bg-2015.jpg"
catalog: true
categories:
    - 技术规范
    - 研发流程
tags:
    - RESTful API
    - 接口文档
    - BED

---

*本文档详细定义孩宝接口，作为接口调用者和实现者的重要参考。*

## 接口文档地址
**[孩宝接口文档地址](https://api.baobaobooks.net/docs/account/)**


## 接口风格
**遵循RESTful设计风格，同时控制复杂度及易于使用，仅遵循大部分原则。**
**遵循原则：**  
- 使用https协议
- 版本号放入URL
- 只提供json返回格式
- post,put上使用json作为输入
- 使用http状态码作为错误提示
- Path（路径）尽量使用名词，不使用动词，把每个URL看成一个资源
- 使用HTTP动词（GET,POST,PUT,DELETE）作为action操作URL资源
- 过滤信息
  - limit：指定返回记录数量
  - offset：记录开始位置
  - direction：请求数据的方向，取值prev-上一页数据；next-下一页数据
  - page：第几页
  - per_page：每页条数
  - total_count：总记录数	
  - total_pages：总页数，等于page时，表示当前是最后一页
  - next\_page：下一页，next\_page > total\_pages时是最后一页
  - sort：column1,column2排序字段
  - orderby：排序规则，desc或asc
  - q：搜索关键字（uri encode之后的）
- 返回结果
  - GET：返回资源对象
  - POST：返回新生成的资源对象
  - PUT：返回完整的资源对象
  - DELETE：返回一个空文档
- 速率限制
  - X-RateLimit-Limit: 每个IP每个时间窗口最大请求数
  - X-RateLimit-Remaining: 当前时间窗口剩余请求数
  - X-RateLimit-Reset: 下次更新时间窗口的时间（UNIX时间戳），达到下个时间窗口时，Remaining恢复为Limit

**未遵循原则：**
- Hypermedia API（HATEOAS），通过接口URL获取接口地址及帮助文档地址信息
- 限制返回值的域，fields=id,subject,customer_name
- 缓存，使用ETag和Last-Modified

**参考：**
[GitHub api ](https://developer.github.com/v3/)
[ruanyifeng blog](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)
[best-practices-for-a-pragmatic-restful-api](http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)


## 模块和版本说明
接口模块相互对立且有版本管理，**模块名作为APP配置项进行存储，每个模块的版本号version和endpoint在应用初始化时调用[api模块信息](https://api.baobaobooks.net/docs/open/#api-basicGroup-get_basic_apis)接口获取并长时间存储**。  
- **凯迪克电商模块及最新版本号：**

模块 | 模块用途 | 最新版本号
:----------- | :----------- | :-----------
account     |帐户            |v1
 ~~ayb~~             | ~~爱阅帮（已废弃）~~          | ~~v2~~ 
sms            |短信            |v1
shop           |电商            |v1
u                 |推广人（孩宝U站）            |v1
www           |官网            |v1
daixiao        |代销            |v1
payment     |支付            |v1
open            |一些开放接口，不需要公共参数            |v1

- **孩宝小镇模块及最新版本号：**

模块 | 模块用途 | 最新版本号
:----------- | :----------- | :-----------
readerclub  |阅读圈        |v1
course        |课堂            |v1
bookshelf   |书架            |v1
user            |阅读家庭（用户数据）            |v1
open            |一些开放接口，不需要公共参数            |v1

## 公共参数
#### Headers
公共请求参数是指每个接口都可能需要传递的参数，公共参数通过header传递。

参数 | 是否必须 | 说明及header格式
:----------- | :----------- | :-----------
ClientType | 所有接口必须（open除外）    |请求客户端标识，取值`haibao-ios、haibao-android…`<br/>header格式：<br/>`X-HB-Client-Type: ClientType`
user_id       |**App登录后所有接口都传**，<br/>Web通过session机制获取 |用户标识<br/>header格式：<br/>`Authorization: HBAPI base64(user_id:token)`
token         |**App登录后所有接口都传**，<br/>Web通过session机制获取 |授权访问令牌<br/>header格式：<br/>`Authorization: HBAPI base64(user_id:token)`

- **Web应用通过cookies传递session id，user_id和token无需传递，接口会从session自动获取；**
- **同一token值在App和Web各应用间通用（token即为session id）；**
- **APP修改user-agent，在原有user-agent的尾部添加`$clientType/$version`和`NetType/$value`。**如：
  - `Dalvik/2.1.0 (Linux; U; Android 6.0.1; MI 4LTE MIUI/V7.5.3.0.MXGCNDE) haibao-android/3.0.0 NetType/4G`
  - `Mozilla/5.0 (iPhone; CPU iPhone OS 10_3_2 like Mac OS X) AppleWebKit/603.2.4 (KHTML, like Gecko) haibao-ios/3.0.0 NetType/WIFI`

- **ClientType取值及释义**

凯迪克电商ClientType取值 | 客户端名称【域名】
:----------- | :----------- 
www-pc        | 官网PC版【www.baobaobooks.com】
www-mobile| 官网手机版【www.baobaobooks.com】
u-pc           | “U站”PC版 【u.baobaobooks.com】
u-ios (~~store-ios~~)        | “U站”iOS版
u-android (~~store-android~~) | “U站”Android版
shop-pc          |  童书馆PC版【*.baobaobooks.com】
shop-mobile  |  童书馆手机版【*.baobaobooks.com】
daixiao-pc| 代销PC版【daixiao.baobaobooks.com】
daixiao-ios| 代销iOS版，暂无
daixiao-android| 代销Android版，暂无
admin-pc| 管理中心PC版【admin.baobaobooks.com】
~~zl-pc~~                | ~~专栏PC版~~
~~zl-mobile~~        |  ~~专栏手机版~~

孩宝小镇ClientType取值 | 客户端名称【域名】
:----------- | :----------- 
haibao-pc        | 孩宝官网/WebPC版【www.hbtown.com】
haibao-mobile| 孩宝官网/Web手机版【www.hbtown.com】
hbu-ios      | 孩宝U站iOS版
hbu-android | 孩宝U站Android版
haibao-ios (~~ayb-ios~~)            | 孩宝小镇iOS版
haibao-android (~~ayb-android~~)    | 孩宝小镇Android版
hbadmin-pc| 孩宝管理中心PC版【admin.hbtown.com】

#### Cookies
- **用于告知服务端是否支持Webp的Cookie：**cookie name是`supportWebp`，取值是1（支持）和0（不支持），未传递时服务端默认取值为0。
- **Webview植入Session的Cookie：**参考：[凯迪克孩宝小镇Hybird App 开发集成规范说明](https://hbtown.worktile.com/drive/58a18aed5aeb7c22b89e6727/58a1523a8fe9534875e595bb)


## 权限
- 权限分为
  - `none`：无需任何授权；
  - `token`：需要孩宝用户登录授权，可通过`header Authorization`和`Cookie HBSID`传递；
  - `admintoken`：需要孩宝管理员登录授权，可通过`header Authorization`和`Cookie HBCPSID`传递；
  - `token || admintoken`：孩宝用户登录授权或孩宝管理员登录授权都可以；
![[小明Martin-产品研发负责人] upload - 2017-04-24 11:11 20.png](https://wt-box.worktile.com/public/cf18ed1a-4324-4ddb-b9ff-39be15a7ac89)
  - `sign`：需要签名，一般用于服务端相互调用，详见[ 孩宝API HMAC-SHA1签名](https://hbtown.worktile.com/drive/58f07f338341595437be627f/58f07f338341595437be62a9)。


## 状态码说明
**正确**  
接口正常访问情况下，服务器返回2××的HTTP状态码。

HTTP状态码|
:----------- |
200 OK - 表示已在响应中发出、资源更改成功（GET、PUT）     |
201 created - 新资源被创建（POST）            |
204 No Content - 资源被删除（DELETE）            |

**错误**  
当用户访问接口出错时，服务器会返回给一个合适的4××或者5××的HTTP状态码；以及一个application/json格式的消息体，消息体中包含错误码code和错误说明message。
- **5××错误(`500=<status code`)为服务器或程序出错，客户端只需要提示“服务异常，请稍后重试”即可，该类错误不在每个接口中列出。**
- **4××错误(`400=<status code<500`)为客户端的请求错误，需要根据具体的code做相应的提示和逻辑处理，message仅供开发时参考，不建议作为用户提示。**
- 部分错误示例：

code | message | HTTP状态码
:----------- | :----------- | :-----------
InvalidToken	|未登录或授权过期，请登录	|401 Unauthorized
ValidationError	|输入字段验证出错，缺少字段或字段格式有误	|422 Unprocessable Entity
AccountNotExist	|账户名不存在	|404 Not Found
InvalidPassword	|密码错误	|401 Unauthorized
NotFound	|请求的资源不存在	|404 Not Found
AccountHasExist	|账户名已经存在	|409 Conflict
MobileHasBinded	|手机号已经绑定其他账户	|409 Conflict
EmptyPassword	|账户未激活，请先激活账号	|403 Forbidden
InvalidSign	|参数签名验证未通过	|403 Forbidden
InvalidSMSCode	|短信验证码错误	|403 Forbidden
ExpiredSMSCode	|过期的短信验证码	|403 Forbidden
FrequencyLimit	|发送过于频繁，请稍后再试	|403 Forbidden
TimesExceeded	|达到最大发送次数限制，请明天再试	|403 Forbidden
VerifyTimesExceeded	|达到最大校验次数，请明天再试	|403 Forbidden
RateLimitExceeded	|接口调用次数超过限制，请稍后再试	|429 Too Many Requests
    |    |
InternalError	|服务异常，请稍后再试	|500 Internal Server Error

- [HTTP状态码参考](http://baike.baidu.com/item/HTTP%E7%8A%B6%E6%80%81%E7%A0%81)
 ![图片](https://dn-coding-net-production-pp.qbox.me/66562d65-3c2b-453b-8d0f-61b03685bc45.png) 


## 参数传递
遵循RESTful规范，使用了GET, POST, PUT, DELETE共4种请求方法。

1. GET：请求资源，返回资源对象
2. POST：新建资源，返回新生成的资源对象
3. PUT：新建/更新资源，返回完整的资源对象
4. DELETE：删除资源，返回body为空

* GET请求不允许有body， 所有参数通过拼接在URL之后传递，**所有的请求参数都要进行遵循[RFC 3986](https://tools.ietf.org/html/rfc3986)的URL Encode**。
* DELETE删除单个资源时，资源标识通过path传递，批量删除时，通过在body中传递JSON。
* POST, PUT请求，所有参数通过JSON传递，*可选的请求参数，只传有值的，无值的不要传递*，contentType为application/json。

*4种请求动作中，GET、PUT、DELETE是幂等的；只有POST是非幂等的。幂等操作的特点是其任意多次执行所产生的影响均与一次执行的影响相同。* **是非幂等是判断接口使用POST还是PUT的决定条件**

**注意： APP端获取json数据时，对于数值类型字段必须以数值类型转换，无论传递过来的值是否带引号。**
 ![图片](https://dn-coding-net-production-pp.qbox.me/aa98e49c-e758-49d1-9fe7-771ac681e4af.png) 
 ![图片](https://dn-coding-net-production-pp.qbox.me/b0936c9b-c5df-4e87-aa5d-6b12a7202f44.png) 


## 速率限制Rate Limiting
- 为了防止API被恶意调用，对API调用进行速率限制。
- 速率限制为每IP每15分钟5000次（dev/qa为10W）调用（15分钟是一个时间窗口）。
- 限制是针对孩宝所有接口模块一起计算的（Redis key为`APIRL:{IP}`），暂时没有特殊的模块或单个接口（未来可能有）。
- 你可以通过每个接口返回的HTTP headers了解当前速率限制的情况:
  - X-RateLimit-Limit: 每个IP每个时间窗口最大请求数
  - X-RateLimit-Remaining: 当前时间窗口剩余请求数
  - X-RateLimit-Reset: 下次更新时间窗口的时间（UNIX时间戳），达到下个时间窗口时，Remaining恢复为Limit
- 超出速率限制，返回以下错误
![[小明Martin-产品研发负责人] upload - 2017-04-13 17:32 41.png](https://wt-box.worktile.com/public/5ad5e735-afd1-4b8f-9cc4-75448304eb52)


## 安全注意事项
- 用户登录后用户的token；aliyun OSS的bucket、AccessKey ID与AccessKey secret；微视频的appid、sign、bucket；这些关键数据通过调用接口获得，需要在客户端以安全的方式存储。
- 音频视频在APP内的存储，不允许被拷贝（即使越狱或root后拿走也无法使用）。

## 测试工具
推荐Chrome浏览器插件Postman作为接口测试工具，**有一个公共账号（所有已有接口在该账号里都有collections）联系Martin获取**。  
[Postman下载地址](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)  
 ![图片](https://dn-coding-net-production-pp.qbox.me/90bcf5b2-745f-465a-9060-c98f6e781e9f.png) 


## 文档生成工具
- 生成的工具为apidoc，详细阅读官方文档：http://apidocjs.com


## 调用示例
- 伪代码
![[小明Martin-产品研发负责人] upload - 2017-04-13 16:44 47.png](https://wt-box.worktile.com/public/99d95dc3-447b-4e5c-9257-020656dbe637)


- PHP
![[小明Martin-产品研发负责人] upload - 2017-04-13 16:33 28.png](https://wt-box.worktile.com/public/8268183a-2cfb-4e48-9016-959a72f68b7d)


## API模块信息获取
- App配置文件中仅存储api模块名，App初始化时请求[获取api模块信息](https://apidev.baobaobooks.net/docs/open/#api-basicGroup-get_basic_apis)，获取各个api模块的信息（uri和version）。