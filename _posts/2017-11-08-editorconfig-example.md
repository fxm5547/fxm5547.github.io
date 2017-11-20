---
layout:     post
title:      "editorconfig配置文件实例"
subtitle:   "editorconfig配置文件实例"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-2015.jpg"
catalog: true
categories:
    - 技术规范
    - 工具手册
tags:
    - editorconfig
---

## [.editorconfig](http://editorconfig.org/)文件规范
editorconfig是一个可以制定统一规范的配置文件，绝大多数代码编辑器都已经支持

配置成使用2个空格的缩进
UTF-8文件编码
lf文件尾
新项目直接拷贝以下代码至根目录下.editorconfig文件即可

```
# http://editorconfig.org

# A special property that should be specified at the top of the file outside of
# any sections. Set to true to stop .editor config file search on current file
root = true

[*]
# Indentation style
# Possible values - tab, space
indent_style = space

# Indentation size in single-spaced characters
# Possible values - an integer, tab
indent_size = 2

# Line ending file format
# Possible values - lf, crlf, cr
end_of_line = lf

# File character encoding
# Possible values - latin1, utf-8, utf-16be, utf-16le
charset = utf-8

# Denotes whether to trim whitespace at the end of lines
# Possible values - true, false
trim_trailing_whitespace = true

# Denotes whether file should end with a newline
# Possible values - true, false
insert_final_newline = true

```