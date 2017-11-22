---
layout:     post
title:      "使用SSH key免密码登录服务器"
subtitle:   "使用SSH RSA key免密码登录Linux服务器"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 工具手册
tags:
    - SSH
    - RSA
---

*适用所有Linux和Mac*

以下以A免密码登录B为例说明。

## 在A生成密钥
*之前已经生成，忽略此步*
`ssh-keygen -t rsa`
一路回车，按默认不更改。

## 放置公钥到B
在A上拷贝前一步生成的公钥：
`vim ~/.ssh/id_rsa.pub`
添加至B的需要被登录的帐户的authorized_keys文件尾部：
`vim ~/.ssh/authorized_keys`

## 配置A的ssh config文件
`vim ~/.ssh/config`
在尾部添加以下内容
```
Host        stage
    HostName        118.178.240.1
    Port            22
    User            root
    PreferredAuthentications publickey
    IdentityFile    ~/.ssh/id_rsa
```

## 完成
 之后，在A上可以免密码轻松登录B：
`ssh stage`
stage就是ssh config文件里配置的Host。