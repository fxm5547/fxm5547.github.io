---
layout:     post
title:      "CSS编码规范"
subtitle:   "良好的CSS编码习惯和风格"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
tags:
    - CSS
    - FED
---

## 使用css-modules
[css-modules](https://github.com/css-modules/css-modules)
<img src="https://raw.githubusercontent.com/css-modules/logos/master/css-modules-logo.png" width="150" height="150" />
- 保留了很好的组件复用性
- 消除了全局命名的问题，在组件的 index.css 中可以随意起名字，不用担心命名冲突
- 和react 结合很好
- 很方便的按需加载
最好使用单一的英文单词命名，不需要使用BEM这类命名方式

## 使用SASS书写css
所有SASS文件根据模块提供必要样式，经由css-modules处理后形成唯一的类
代码格式如下（注意空格）:
所有文件均由[.editorconfig](http://editorconfig.org/)文件统一格式化
```style
.foo {
  background: #fff;

  &.active {
    color: #000;
  }
}
```

## 尽可能使用Class选择器
没有必要使用ID选择器，子选择器中可以使用tag（标签）选择器