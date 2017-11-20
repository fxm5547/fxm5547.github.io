---
layout:     post
title:      "Shadowsocks翻墙使用手册"
subtitle:   "Shadowsocks安装配置入门指南"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-2015.jpg"
catalog: true
categories:
    - 工具手册
tags:
    - Shadowsocks
    - 使用手册
---

## 下载shadowsocks客户端
Windows： 链接: http://pan.baidu.com/s/1pJL0Z8n 密码: jwtc
Mac OS X：http://dwz.cn/3FwvRR
Android：http://dwz.cn/3DV3Ei
iOS：http://dwz.cn/3FwvnF

## 配置账号（Windows）
打开shadowsocks客户端之后，按照下图指示扫描下文的二维码（多扫几个，出问题时切换）。

 ![图片](https://dn-coding-net-production-pp.qbox.me/32a2d1ad-7816-46e9-a87b-46ae61d2fd17.png) 

- 线路购买
  - 稳定快速的线路购买，推荐：<http://108.61.186.155>

## 选择代理模式（Windows）
右键点击任务栏右下角的shadowsocks客户端图标，请确保“启用系统代理”被选中，如下图所示

 ![图片](https://dn-coding-net-production-pp.qbox.me/9f9ac3ad-fb30-491c-94d0-ba4a0c65ff17.png) 

**“系统代理模式”选择“PAC模式”**（全局模式将导致本机所有网络请求都通过该代理，而PAC模式只转发PAC文件中的域名（墙外的域名）请求）。

 ![图片](https://dn-coding-net-production-pp.qbox.me/e4f72815-1c21-4e31-89c5-f0ca933e09f0.png) 

发现有网站无法访问，可以手动编辑PAC文件，将域名加入该文件。

 ![图片](https://dn-coding-net-production-pp.qbox.me/c7f4b299-3ce1-4513-bf4a-8a3d95ed3c87.png) 

## 切换服务器（Windows）
在当前线路慢或无法代理时，可以切换线路（服务器）

 ![图片](https://dn-coding-net-production-pp.qbox.me/2355b426-095e-46b2-be63-9e83e8e8a634.png) 


## 配置账号（Mac）
在Launchpad中打开shadowsocks客户端之后（不支持开机启动），按照下图指示扫描上文的二维码（多扫几个，出问题时切换）。
 ![图片](https://dn-coding-net-production-pp.qbox.me/9ed87656-6629-45ae-94dd-2a7178a855b7.png) 

**注意：第一次配置之后，代理有可能不生效，请重启浏览器甚至重启计算机再试**

## 选择代理模式（Mac）
选择“自动代理模式”只代理需要翻墙的域名请求，“全局模式”将导致本机所有网络请求都通过该代理
 ![图片](https://dn-coding-net-production-pp.qbox.me/d126acd4-6bce-4ad0-84d3-6972afb9b129.png) 

发现有网站无法访问，可以手动编辑PAC文件，将域名加入该文件。
 ![图片](https://dn-coding-net-production-pp.qbox.me/9756a0ca-4737-434e-9745-dfb3a3de05aa.png) 


## 切换服务器（Mac）

在当前线路慢或无法代理时，可以切换线路（服务器）

 ![图片](https://dn-coding-net-production-pp.qbox.me/6d73a61f-3afc-4187-9d61-a061037c4895.png)