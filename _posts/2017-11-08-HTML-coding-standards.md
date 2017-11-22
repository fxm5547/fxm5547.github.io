---
layout:     post
title:      "HTML编码规范"
subtitle:   "HTML良好的编码风格"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
tags:
    - HTML
    - FED
---

# HTML编码规范

## 1 前言


HTML作为描述网页结构的超文本标记语言，在百度一直有着广泛的应用。本文档的目标是使HTML代码风格保持一致，容易被理解和被维护。




## 2 代码风格

使用 `2` 个空格做为一个缩进层级，不允许使用 `4` 个空格 或 `tab` 字符。
.editorconfig自动配置


示例：

```html
<ul>
  <li>first</li>
  <li>second</li>
</ul>
```

每行不得超过 `120` 个字符。

解释：

过长的代码不容易阅读与维护。但是考虑到 HTML 的特殊性，不做硬性要求。

## 3 标签名必须使用小写
示例：
```html
<!-- good -->
<p>Hello StyleGuide!</p>

<!-- bad -->
<P>Hello StyleGuide!</P>
```

## 4 对于无需自闭合的标签，必须闭合
常见无需自闭合标签有input、br、img、hr等。
示例：
```html
<!-- good -->
<input type="text" name="title" />

<!-- bad -->
<input type="text" name="title">
```

## 5 HTML 标签的使用应该遵循标签的语义
- p - 段落
- h1,h2,h3,h4,h5,h6 - 层级标题
- strong,em - 强调
- ins - 插入
- del - 删除
- abbr - 缩写
- code - 代码标识
- cite - 引述来源作品的标题
- q - 引用
- blockquote - 一段或长篇引用
- ul - 无序列表
- ol - 有序列表
- dl,dt,dd - 定义列表

示例：
```html
<!-- good -->
<p>Esprima serves as an important <strong>building block</strong> for some JavaScript language tools.</p>

<!-- bad -->
<div>Esprima serves as an important <span class="strong">building block</span> for some JavaScript language tools.</div>
```

## 6 标签的使用应尽量简洁，减少不必要的标签
示例：
```html
<!-- good -->
<img class="avatar" src="image.png">

<!-- bad -->
<span class="avatar">
    <img src="image.png">
</span>
```

## 7 属性名必须使用小写字母
示例：
```html
<!-- good -->
<table cellspacing="0">...</table>

<!-- bad -->
<table cellSpacing="0">...</table>
```

## 8 布尔类型的属性，建议不添加属性值
示例：
```html
<input type="text" disabled>
<input type="checkbox" value="1" checked>
```

## 9 自定义属性建议以 xxx- 为前缀，推荐使用 data-
示例：
```html
<ol data-ui-type="Select"></ol>
```

## 10 DOCTYPE
[强制] 使用 HTML5 的 doctype 来启用标准模式，建议使用大写的 DOCTYPE。
示例：
```html
<!DOCTYPE html>
```
启用viewport模式
```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```
启用最新渲染模式
```html
<meta http-equiv="X-UA-Compatible" content="chrome=1,IE=edge">
```

## 10 编码
HTML 文件使用无 BOM 的 UTF-8 编码

## 11 CSS和JavaScript引入
[强制] 引入 CSS 时必须指明 rel="stylesheet"
引入 CSS 和 JavaScript 时无须指明 type 属性
解释：

text/css 和 text/javascript 是 type 的默认值。

在 head 中引入页面需要的所有 CSS 资源。
JavaScript 应当放在页面末尾，或采用异步加载
解释：

将 script 放在页面中间将阻断页面的渲染。出于性能方面的考虑，如非必要，请遵守此条建议。

示例：
```html
<body>
    <!-- a lot of elements -->
    <script src="init-behavior.js"></script>
</body>
```

[建议] 移动环境或只针对现代浏览器设计的 Web 应用，如果引用外部资源的 URL 协议部分与页面相同，建议省略协议前缀。

解释：

使用 protocol-relative URL 引入 CSS，在 IE7/8 下，会发两次请求。是否使用 protocol-relative URL 应充分考虑页面针对的环境。

示例：
```html
<script src="//s1.bdstatic.com/cache/static/jquery-1.10.2.min_f2fb5194.js"></script>
```

## 11 head
[强制] 页面必须包含 title 标签声明标题
[强制] title 必须作为 head 的直接子元素，并紧随 charset 声明之后
解释：

title 中如果包含 ascii 之外的字符，浏览器需要知道字符编码类型才能进行解码，否则可能导致乱码。

示例：
```html
<head>
    <meta charset="UTF-8">
    <title>页面标题</title>
</head>
```

## 12 favicon
[强制] 保证 favicon 可访问。

解释：

在未指定 favicon 时，大多数浏览器会请求 Web Server 根目录下的 favicon.ico 。为了保证favicon可访问，避免404，必须遵循以下两种方法之一：

- 在 Web Server 根目录放置 favicon.ico 文件。
- 使用 link 指定 favicon。

示例：
```html
<link rel="shortcut icon" href="path/to/favicon.ico">
```

## 13 图片
[强制] 禁止 img 的 src 取值为空。延迟加载的图片也要增加默认的 src。

解释：

src 取值为空，会导致部分浏览器重新加载一次当前页面，参考：https://developer.yahoo.com/performance/rules.html#emptysrc

[建议] 避免为 img 添加不必要的 title 属性。

解释：

多余的 title 影响看图体验，并且增加了页面尺寸。

[建议] 为重要图片添加 alt 属性。

解释：

可以提高图片加载失败时的用户体验。

[建议] 添加 width 和 height 属性，以避免页面抖动。

[建议] 有下载需求的图片采用 img 标签实现，无下载需求的图片采用 CSS 背景图实现。

解释：

- 产品 logo、用户头像、用户产生的图片等有潜在下载需求的图片，以 img 形式实现，能方便用户下载。
- 无下载需求的图片，比如：icon、背景、代码使用的图片等，尽可能采用 css 背景图实现。

## 14 表单
[强制] 有文本标题的控件必须使用 label 标签将其与其标题相关联
解释：

有两种方式：

- 将控件置于 label 内。
- label 的 for 属性指向控件的 id。
推荐使用第一种，减少不必要的 id。如果 DOM 结构不允许直接嵌套，则应使用第二种。

示例：

```html
<label><input type="checkbox" name="confirm" value="on"> 我已确认上述条款</label>

<label for="username">用户名：</label> <input type="textbox" name="username" id="username">
```

[强制] 使用 button 元素时必须指明 type 属性值。

解释：

button 元素的默认 type 为 submit，如果被置于 form 元素中，点击后将导致表单提交。为显示区分其作用方便理解，必须给出 type 属性。

示例：
```html
<button type="submit">提交</button>
<button type="button">取消</button>
```

## 15 模板中的 HTML
[建议] 模板代码的缩进优先保证 HTML 代码的缩进规则

示例：
```html
<!-- good -->
{if $display == true}
<div>
    <ul>
    {foreach $item_list as $item}
        <li>{$item.name}<li>
    {/foreach}
    </ul>
</div>
{/if}

<!-- bad -->
{if $display == true}
    <div>
        <ul>
    {foreach $item_list as $item}
        <li>{$item.name}<li>
    {/foreach}
        </ul>
    </div>
{/if}
```