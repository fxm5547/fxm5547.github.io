---
layout:     post
title:      "JS编码规范"
subtitle:   "良好的JS编码习惯与风格"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
tags:
    - JavaScript
    - FED
---

## 格式
每句js后无需加`;`
赋值`=`号前后加空格
示例:
```js
const RECEIVE_ZEN = 'RECEIVE_ZEN'
const REQUEST_ZEN = 'REQUEST_ZEN'
const CLEAR_ZEN = 'CLEAR_ZEN'
```

## 使用Babel来写ES6/7代码
ES6/7新增了很多新特性，让我们可以更好的来编写javascript
使用[Babel](https://babeljs.io/)我们可以编写ES6/7最终编译成ES5，保证不存在兼容性问题

## 尽可能减少使用jQuery
jQuery已经慢慢淡出我们的视线了
[youmightnotneedjquery](https://github.com/HubSpot/youmightnotneedjquery)
[You-Dont-Need-jQuery](https://github.com/oneuijs/You-Dont-Need-jQuery)

## 使用函数式编程吧
[JS函数式编程指南](https://www.gitbook.com/book/llh911001/mostly-adequate-guide-chinese/details)
[Javascript函数式编程风格](http://www.ruanyifeng.com/blog/2012/04/javascript_programming_style.html)

## 使用ES6的模块机制
引入
`import foo from 'module'`
导出
```js
const foo = {
  ...
}
export default foo
```

## defer与async
`<script src="script.js"></script>`
没有 defer 或 async，浏览器会立即加载并执行指定的脚本，“立即”指的是在渲染该 script 标签之下的文档元素之前，也就是说不等待后续载入的文档元素，读到就加载并执行。

`<script async src="script.js"></script>`
有 async，加载和渲染后续文档元素的过程将和 script.js 的加载与执行并行进行（异步）。

`<script defer src="script.js"></script>`
有 defer，加载后续文档元素的过程将和 script.js 的加载并行进行（异步），但是 script.js 的执行要在所有元素解析完成之后，DOMContentLoaded 事件触发之前完成。

它俩的差别在于脚本下载完之后何时执行，显然 defer 是最接近我们对于应用脚本加载和执行的要求的

关于 defer，关键一点在于它是按照加载顺序执行脚本的，这一点要善加利用

async 则是一个乱序执行的主，反正对它来说脚本的加载和执行是紧紧挨着的，所以不管你声明的顺序如何，只要它加载完了就会立刻执行

仔细想想，async 对于应用脚本的用处不大，因为它完全不考虑依赖（哪怕是最低级的顺序执行），不过它对于那些可以不依赖任何脚本或不被任何脚本依赖的脚本来说却是非常合适的，最典型的例子：Google Analytics

所以我们工作中大多数加载script的地方都可以用defer取代