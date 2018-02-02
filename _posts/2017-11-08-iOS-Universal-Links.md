---
layout:     post
title:      "iOS Universal Links实现方案"
subtitle:   "iOS Universal Links实现微信内网页跳转至App的方案"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
tags:
    - Universal Links
    - iOS
---

## 配置方法
1. 生成文件名为apple-app-site-association的json文件，文件名不允许有类型后缀，上传到服务器根目录，需要满足访问https:domain.com/apple-app-site-association 能够下载或者打开json内容
2. json文件中定义了app支持的路径，如path写/bookshelf/*，那么用户点击https://www.url.com/bookshelf/10086，就可以直接跳转到app

```
 {
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "GF72L9K2ER.com.caldecott.haibao",
                "paths": [ "/bookshelf/*、”, "/users/*"]
            }
        ]
    }
} 
```

## 适用范围
1. iOS9以后,iOS9以前的版本还是需要通过scheme的方式进行跳转
2. 在相同的domain内Universal Links是无效的，至少要跨子域才生效。比如 m.domain.com 跳转 o.domain.com 可以触发跳转App。抓取知乎的链接为例，分享到微信的url为https://www.zhihu.com/question/61752144。点击app内打开，跳转的url为https://oia.zhihu.com/questions/61752144

## Web适配
1. oia.hbtown.com任意path都访问以下这页，可带scheme在app中打
 
 ![图片](https://dn-coding-net-production-pp.qbox.me/4045ba66-a93b-4439-9646-eb876938b463.png) 

2. oia.hbtown.com根目录下放置json文件`apple-app-site-association`，放到工程里git管理。
3. 所有对应Web页面的“打开App”的链接都修改为oia.hbtown.com加当前页面的path，并传参scheme，如：

 ![图片](https://dn-coding-net-production-pp.qbox.me/b73b6e6c-09a2-4e64-bbd4-5ed4ccf7650e.png)