---
layout:     post
title:      "Charles使用手册"
subtitle:   "Charles的安装配置入门指南"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 工具手册
tags:
    - Charles
    - 使用手册
---

## Charles是什么 
是在 Mac或Windows下常用的网络包截取工具,在平常的测试与调式过程中,掌握此工具就基本可以不用其他抓包工具了。 有不同平台的版本（Mac, Windows、Linux）。

## Charles的下载和安装过程 
- 下载地址：http://www.charlesproxy.com/download/ 
- 破解：[破解方法](http://www.jianshu.com/p/89111882fa99) 

## HTTPS配置步骤 
- 打开Help-SSL Proxying
- 电脑端安装证书，在本机钥匙串访问中设置为信任。 
 ![图片](https://dn-coding-net-production-pp.qbox.me/b1de563a-b4e6-4cbd-93ac-d72be5eda7e7.png?imageView2/0/w/600) 
 ![图片](https://dn-coding-net-production-pp.qbox.me/9ac31a48-4d5f-4724-95c1-c733a74b12b8.png?imageView2/0/w/600) 
- 手机浏览器访问<http://chls.pro/ssl>安装证书 
 ![图片](https://dn-coding-net-production-pp.qbox.me/c23a5059-8999-47b4-b719-9baa2b0c6af5.png) 
- 设置代理
 ![图片](https://dn-coding-net-production-pp.qbox.me/47dde2a2-12e6-41ac-9133-df45b19bd6fa.png?imageView2/0/w/600) 
 ![图片](https://dn-coding-net-production-pp.qbox.me/145d62c0-c6d9-449f-bf80-a1562024a24c.png?imageView2/0/w/600) 


## APP抓包
- 手机和电脑连入同一局域网
- 手机端设置HTTP代理 
  - Android
 ![图片](https://dn-coding-net-production-pp.qbox.me/94115abe-2d90-4b2d-87a6-437e56ebc5e9.png?imageView2/0/w/600) 
  - IOS 
 ![图片](https://dn-coding-net-production-pp.qbox.me/416f0033-0ccd-4851-a4ef-f9c5ddd920d0.png?imageView2/0/w/600) 