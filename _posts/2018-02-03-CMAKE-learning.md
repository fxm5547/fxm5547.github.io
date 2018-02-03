---
layout:     post
title:      "CMake入门指南"
subtitle:   "CMake简易入门"
date:       2018-02-03 16:00:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 工具手册
    - 技术规范
tags:
    - CMake
    - 学习指南
---

## 参考
- 官方手册：<https://cmake.org/>
- CMake 入门实战：<http://www.hahack.com/codes/cmake/>

## CMake简介
- Makefile是类unix环境下的类似于批处理的"脚本"文件。其基本语法是: 目标+依赖+命令，只有在目标文件不存在，或目标比依赖的文件更旧，命令才会被执行。
- make是用来执行Makefile的.
- Makefile+make可理解为类unix环境下的项目管理工具，但它太基础了，抽象程度不高，而且在windows下不太友好，于是就有了跨平台项目管理工具CMake， CMake是抽象层次更高的项目管理工具，CMake命令执行的CMakeLists.txt文件，生成Makefile。
- >CMake is great. don't waste time on other C++ build tools, seriously.
- CMake是CLion IDE（JetBrains出品）唯一默认支持的构建工具。

## 实例
- 工程结构
 ![图片](https://dn-coding-net-production-pp.qbox.me/396d6036-cf32-4f08-9a52-d56773a987af.png?imageView2/0/w/400) 
- 代码文件都在src目录
- CMakeLists.txt文件是使用CMake需要编写的唯一文件：

```
cmake_minimum_required(VERSION 2.6)
project(itest)

# C++标准
set(CMAKE_CXX_STANDARD 11)

# 指定参与编译的源文件
add_executable(itest src/main.cpp src/cal/Calculator.cpp src/cal/Calculator.h)

# 指定安装路径，make install 时运用
install (TARGETS itest DESTINATION bin)
install(DIRECTORY src/ DESTINATION include/itest FILES_MATCHING PATTERN "*.h")

# 设置不同build类别时的编译参数
#set(CMAKE_BUILD_TYPE "Debug")
set(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
```
- debug和release是存放编译中间和结果文件夹，cmake.sh是一个执行cmake和make命令的脚本：

```
#!/bin/bash

# 父级目录
base_dir=$(dirname $(pwd))

# 制定构建类型是debug
cmake $base_dir -DCMAKE_BUILD_TYPE=Debug

# 编译
make
```
- 执行`chmod a+x cmake.sh && ./cmake.sh`，完成整个构建过程，生成itest可执行程序
 ![图片](https://dn-coding-net-production-pp.qbox.me/8c21ec72-971d-470d-8736-c05bf0ac7803.png) 








