---
layout:     post
title:      "RESTful API 授权签名规范"
subtitle:   "基于HMAC-SHA1的RESTful API 授权签名方法"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
tags:
    - RESTful
    - API
    - 签名
    - BED
---

## 引言
为了避免API被非法调用，调用过程中被篡改和重放攻击，需要增加API调用授权。对调用信息进行签名和验签是常用的授权方法。调用双方约定秘钥并内部存放，利用秘钥基于hash算法（常用的有MD5，SHA1和SHA256）通过HMAC运算生产签名signature。

## 参考
- <http://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html>
- <https://help.aliyun.com/document_detail/25492.html?spm=5176.doc25489.6.813.MWT9Wx>
- <https://help.aliyun.com/document_detail/31951.html?spm=5176.doc31950.6.832.toV9bg>
- <http://docs.aws.amazon.com/AmazonS3/latest/dev/RESTAuthentication.html>
- <https://www.qcloud.com/document/api/377/4214>

## 传递方式
- 通过header传递，格式：`Authorization: CoAPI-HMAC-SHA1 $sign`
- 同时传递header `X-Co-TimeStamp`，格式：`X-Co-TimeStamp: 1493030704`

## 签名过程
```
$sign = base64(hmac-sha1(SecretKey,
            HTTPRequestMethod + "\n"
            + CanonicalURI + "\n"
            + CanonicalQueryString + "\n"
            + CanonicalHeaders + "\n"
            + CanonicalBody))
```
- `SecretKey` 表示签名所需的密钥，服务端存储不传递；
- `HTTPRequestMethod` 表示HTTP 请求的Method，主要有GET，POST，PUT，DELETE， HEAD，OPTION等，使用大写；
- `\n`表示换行符；
- `CanonicalURI` 表示格式化后的请求URI=`Host + path`，`path`使用`/`开头（即使后面为空）。例子：`api.url.com/shop/v1/goods/9642`；
- `CanonicalQueryString` 表示格式化后的请求参数字符串，可为空。对请求参数按照key的字典序排列(PHP的ksort())后，进行以下拼接
```
CanonicalQueryString = (key1=urlEncode(val1)&key2=urlEncode(val2)...)
```
`urlEncode`指遵循[RFC 3986](https://tools.ietf.org/html/rfc3986)的URL Encode（PHP中的rawurlencode()）。
- `CanonicalHeaders` 表示格式化后的Headers，只使用`X-Co-App`和`X-Co-TimeStamp`，
```
CanonicalHeaders = lower("X-Co-App") + ':' + trim(HeaderValue) + "\n"
                   + lower("X-Co-TimeStamp") + ':' + trim(HeaderValue)
```
`lower()`表示转换为小写，`trim()`表示去除前后空格。
- `CanonicalBody` 表示格式后的Body，可为空。API的Body都是Json，对Json的第一层元素按照key的字典序排列(PHP的ksort())后，进行以下拼接
```
CanonicalBody = (key1=val1&kay2=val2...)
```
如果value是对象或数组，对其进行json encode。
## 签名验证失败
-  如果Header中的`X-Co-TimeStamp`和服务器的时间差15分钟以上，拒绝该服务，并返回`InvalidSign 签名已过期`错误；
- 签名错误，拒绝该服务，并返回`InvalidSign 签名校验错误`错误。