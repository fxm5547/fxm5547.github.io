---
layout:     post
title:      ""
subtitle:   ""
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-2015.jpg"
catalog: true
categories:
    - 技术规范
tags:
    - 产品研发流程
    - Scrum敏捷开发
---

# 孩宝Hybrid App 开发集成规范说明

## 1. 前导说明

本方案是孩宝和凯迪克电商相关App内集成WebView时统一实现原生及HTML交互的规范说明，以供开发、测试时作为规范及参考。


## 2. 关于Hybrid App框架说明

目前有较多的Hybrid App开发框架，有偏重Web型的，也有偏重native型的，总的来说，都是利用HTML+CSS+JavaScript快速开发迭代和可热更新的优势，同时又能有效使用原生系统特有功能。

在这些框架中，有[PhoneGap]( http://phonegap.com/)、[React Native](https://facebook.github.io/react-native/)等为典型代表。其中PhoneGap型采用统一封装的superWebView方式进行跨平台开发，以中间件的形式连接JavaScript和原生系统API，这种方式非常依赖于中间件。而React Native 型则是直接底层封装了原生系统的各种API后提供给开发者以JavaScript开发native App的能力，其最终发布的产品跟native App并无多少区别。但是其缺点也非常明显，开发时使用的API必须是框架开发完成的。

## 3. 集成规范说明

本次集成采用WebView的方式自定义封装一个可提供原生代码（Java或Objective-C）与JavaScript代码通信的bridge壳，即提供给Web页面调用与原生功能的交互能力。

**在集成过程中，有些问题需要特别注意，特别是安全问题，在Web App和bridge壳交互时，必须做严格的来源及数据合法性校验。该集成主要采用WebView注入JavaScript代码以供Web App调用的方式进行，这样的好处是能快速开发上线，坏处则是需要对iOS和Android分别处理。**

下面对集成过程中的这些事项进行详细说明。

### 3.1 客户端识别

本次集成除了App外，原Web App还需兼容移动端浏览器，故bridge壳需另外设置请求头的User-Agent，以便识别请求客户端。设置时，统一在User-Agent设置客户端名称、客户端版本号及网络类型。即在原有user-agent的尾部添加`$app/$version`和`NetType/$value`。
具体规范如下表：

|App|app|User-Agent示例|
|:--|:---:|:---|:---|
|孩宝小镇iOS|haibao-ios|Mozilla/5.0 (iPhone; CPU iPhone OS 10_0_1 like Mac OS X) AppleWebKit/602.1.50 (KHTML, like Gecko) **haibao-ios/2.4.2 NetType/WIFI**|
|孩宝小镇android|haibao-android|Mozilla/5.0 (Linux; Android 5.1.1; SAMSUNG SM-A7100 Build/LMY47X) SamsungBrowser/4.0 Chrome/44.0.2403.133 Mobile Safari/537.36 **haibao-android/2.4.2 NetType/4G**|
|孩宝U站iOS|hbu-ios|Mozilla/5.0 (iPhone; CPU iPhone OS 10_0_1 like Mac OS X) AppleWebKit/602.1.50 (KHTML, like Gecko) **hbu-ios/2.4.2 NetType/WIFI**|
|孩宝U站android|hbu-android|Mozilla/5.0 (Linux; Android 5.1.1; SAMSUNG SM-A7100 Build/LMY47X) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/4.0 Chrome/44.0.2403.133 Mobile Safari/537.36 **hbu-android/2.4.2 NetType/WIFI**|
|凯图U站iOS|u-ios|Mozilla/5.0 (iPhone; CPU iPhone OS 10_0_1 like Mac OS X) AppleWebKit/602.1.50 (KHTML, like Gecko) **u-ios/2.4.2 NetType/3G**|
|凯图U站android|u-android|Mozilla/5.0 (Linux; Android 5.1.1; SAMSUNG SM-A7100 Build/LMY47X) AppleWebKit/537.36 (KHTML, like Gecko) SamsungBrowser/4.0 Chrome/44.0.2403.133 Mobile Safari/537.36 **u-android/2.4.2 NetType/WIFI**|

**注：**针对iOS系统，当前只有iOS 9以上系统支持修改User-Agent，故iOS 9及更低版本系统，只能通过判断User-Agent中是否包含Safari字段来识别是否来至iOS。即：
- 当User-Agent中包含有iPhone/iPod/iPad但没有Safari字段时，请求来至App内嵌bridge壳；
- 当User-Agent中包含有iPhone/iPod/iPad且有Safari字段时，请求来至iOS客户端浏览器。

### 3.2 用户登录

在凯迪克孩宝小相关APP内打开孩宝的Web页面需写入会话保持的cookie，以同步用户登录状态。cookie name是`HBSID`， cookie value是TOKEN，如`Cookie:HBSID=m0tn6rs2mmc68ihml546ghkv93; `  

需要植入cookie的域名有：
  - 开发/测试环境：
    - haibaotown.net
    - baobaobooks.net
    - 示例：
![图片](https://dn-coding-net-production-pp.qbox.me/feae7989-1996-4041-a11c-fb7c2eccebc0.png) 

  - 生产环境：
    - hbtown.com
    - baobaobooks.com
    - 示例：
![图片](https://dn-coding-net-production-pp.qbox.me/00b9eb59-b348-41cb-894f-e6a8ebc286a0.png) 


### 3.3 页面title

在bridge壳中，默认提取当前Web页面的documnet.title为navigationBar的title，故Web App可通过设置Document的title来设置native的页面title。

### 3.4 下拉刷新

在集成时，页面的下拉刷新不需要Web App进行处理，但是bridge壳需要注意处理，当用户进行下拉刷新时，刷新的应该为当前显示的页面，也就是刷新的是当前页面的URL。所以刷新前应先获取WebView当前的URL来进行重新加载。

### 3.5 处理页面跳转

在处理页面跳转时，WebView的浏览历史的功能能让我们实时知道当前能否返回上一个页面或者能否到下一个页面。**当用户点击一次“返回”后，发现history中仍有页面，即显示“关闭”，“关闭”即为退出Webview，回到原生页面**。

另外，对于部分预先定义的，不属于`*.baobaobooks.com`，`*.hbtown.com`，`*.haibaotown.net`，`*.baobaobooks.net`域名下的，需要在bridge壳内PUSH新的Controller（Acitivity）打开。在打开的新页面的导航栏左上角添加返回按钮，返回按钮事件是直接返回原页面，而不是新的Controller（Acitivity）内WebView跳转的记录。

### 3.6 分享

集成分享功能时，Web App 需要根据bridge壳提供的数据交互通道提供分享所必须的数据，以便调用原生的分享功能。

同时，Web App还能决定是否显示原生的分享button（导航栏右上角的分享），即在页面加载完成后，调用如下方法即可：

请求数据：

```javascript
var data = {'is_show':'1'}; // is_show，是否显示，1显示，0不显示
```

iOS端时调用：
``` javascript
window.webkit.messageHandlers.hb_showShareButton.postMessage(data);
```
    
Android端时调用：
```javascript
window.webkit_android.hb_showShareButton(data);
```

下面定义iOS端及Android端提供的native分享功能的JavaScript交互通道。


#### 3.6.1 分享链接

分享时Web App需要提供的数据为：

> * title：分享内容的title，不可空
> * content：分享的内容，可空
> * share_url：分享的URL，不可空，绝对地址
> * image_url：分享的图片地址，可空，绝对地址
> * callback：分享后的回调，Web App提供给bridge回调的函数名，可空

```javascript
 var data = {"title":"小明童书馆","content":"小明童书馆的说明","share_url":"fxm5547.s.baobaobooks.com","image_url":"fxm5545.s.baobaobooks.com/5547/3344.png","callback":"share_callback"};
```
    
iOS端时调用：
``` javascript
window.webkit.messageHandlers.hb_shareContent.postMessage(data);
```
    
Android端时调用：
```javascript
window.webkit_android.hb_shareContent(data);
```

bridge壳在分享成功或失败时，如果Web App提供了参数callback（**注：本文所有的callback对象均必须为window子对象**），则调用该回调函数，回调时返回数据为：
```javascript
{"result":"success"} 或者 {"result":"failure"}
```

#### 3.6.2 分享图书二维码

主要用于孩宝U站中分享商品二维码图片。

分享时Web App需要提供的数据为：

> * goods_name：商品名，不可空
> * share_desc：商品简介，不可空
> * author_name：作者名，可空
> * drawer_name：绘者名，可空
> * recommend_age：适合阅读年龄，可空
> * market_price：市场价，不可空
> * shop_price：零售价，不可空
> * share_qrcode：分享的二维码URL，不可空，绝对地址
> * images：合成图片的图片URL数组，可空，绝对地址
> * callback：分享后的回调，Web App提供给bridge回调的函数名，可空

```javascript
 var data = {"goods_name":"小明童书馆","share_desc":"小明童书馆的说明","share_qrcode":"fxm5547.s.baobaobooks.com","author_name":"安东尼","market_price":"￥128.00","shop_price":"￥98.00","images":["fxm5545.s.baobaobooks.com/5547/3344.png"],"callback":"share_callback"};
```
    
iOS端时调用：
``` javascript
window.webkit.messageHandlers.hb_shareGoodsQrcode.postMessage(data);
```
    
Android端时调用：
```javascript
window.webkit_android.hb_shareGoodsQrcode(data);
```

bridge壳在分享成功或失败时，如果Web App提供了参数callback（**注：本文所有的callback对象均必须为window子对象**），则调用该回调函数，回调时返回数据为：
```javascript
{"result":"success"} 或者 {"result":"failure"}
```


### 3.7 Alert Message

Web App可调用native的Alert功能弹出消息对话框，并在用户做出对应选择后，bridge壳可回调Web App对应处理方法。

Web App调用时，数据格式如下：

> * title：提示的标题，可空
> * content：提示的内容说明，不可空
> * cancel_title：取消按钮的title，不可空
> * cancel_callback：取消的回调操作，Web App提供给bridge壳回调，可空
> * confirm_title：确认按钮的title，可空
> * confirm_callback：确认的回调操作，Web App提供给bridge壳回调，可空

```javascript
var data = {"title":"提示","content":"确定要放弃？","cancel_title":"放弃","cancel_callback":"hb_cancelHandler","confirm_title":"","confirm_callback":"hb_confirmHandler"};
```
    
iOS端时调用：
```javascript
window.webkit.messageHandlers.hb_alert.postMessage(data);
```

Android端时调用：
```javascript
window.webkit_android.hb_alert(data);
```

bridge壳在接收到操作请求后，显示对应的消息，同时等用户做出选择后回调Web App提供的对应回调函数。回调时没有回调数据。


### 3.8 复制到剪贴板

bridge壳提供给Web App设置内容到native剪贴板的方法，目前只支持设置字符串。

Web App调用时，数据格式如下：

> * content：设置的内容，不可空
> * callback：回调函数的名称，可空

```javascript
var data = {"content":"复制到剪贴板","callback":"pasteboard_callback"};
```
    
iOS端时调用：
```javascript
window.webkit.messageHandlers.hb_pasteboard.postMessage(data);
```
Android端时调用：
```javascript
window.webkit_android.hb_pasteboard(data);
```

bridge壳在接收到操作请求后进行对应处理后，如果callback不为空，则bridge壳回调callback，并返回如下结果：
```javascript
{"result":"success"} 或者 {"result":"failure"}
```

### 3.9 自定义消息提示型

bridge壳提供给Web App设置消息提示的接口（不是系统弹出消息样式），目前提供两个样式text显示文字，loading显示加载动画。Web App调用时，数据格式如下：

> * mode：消息类型，取值为loading，text，分别对应不同样式，默认text
> * contet：消息说明，即显示的消息内容，为loading时可空
> * duration：消息显示的时长，默认1s

```javascript
 var data = {"mode":"text","content":"已成功复制链接","duration":"1.5"};
```

iOS端调用时：
```javascript
window.webkit.messageHandlers.hb_showHUD.postMessage(data);
```

Android端调用时：
```javascript
window.webkit_android.hb_showHUD(data);
```

该接口没有回调。