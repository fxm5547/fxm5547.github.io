---
layout:     post
title:      "Composer使用规范"
subtitle:   "Composer使用规范"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-default.jpg"
catalog: true
categories:
    - 技术规范
tags:
    - Composer
---


## 介绍
- Dependency Manager for PHP
- 官网：https://getcomposer.org/
- 安装：https://getcomposer.org/download/
- 文档：https://getcomposer.org/doc/

## 使用
- Composer我们只用于引入第三方库，不包括自己的库（用Phalcon的autoloader），所以使用Composer时一定要Autoloader Optimization，参考：https://getcomposer.org/doc/articles/autoloader-optimization.md
- install:  `composer install --no-dev -a`
- update:  `composer update --no-dev -a`
- require：`composer require package-name -a`
- Laravel的`php artisan optimize --force`包含了Composer的优化。