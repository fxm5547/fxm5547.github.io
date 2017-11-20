---
layout:     post
title:      "PhpStorm基本配置及常用快捷键"
subtitle:   "助你提高代码质量及开发效率的PhpStorm基本配置及常用快捷键"
date:       2017-11-08 14:33:00
author:     "fxm5547"
header-img: "img/post-bg-2015.jpg"
catalog: true
categories:
    - 技术规范
    - 工具手册
tags:
    - PhpStorm
    - 快捷键
    - BED
    - 工具手册
---


## 重要Preference配置
- **激活服务器**
> 
http://jetbrains.tencent.click/
http://owo.help
http://idea.imsxm.com/
http://www.0-php.com:1017

- **安装以下必要插件**
  - Php Inspections (EA Extended)
  - PHP Annotations
  - .ignore
  - Markdown Navigator
  - editorconfig
 ![图片](https://dn-coding-net-production-pp.qbox.me/756747d2-8045-4f4e-8b99-ba5ba9fc3d60.png) 


- **PHP正确版本及解释器（本地安装）**
 ![图片](https://dn-coding-net-production-pp.qbox.me/ee373d91-f008-44ad-a98e-91ffbf6fe661.png) 


- **PHP代码风格选择PSR-1/PSR-2**
 ![图片](https://dn-coding-net-production-pp.qbox.me/1700c3d5-5f64-4a6f-a323-ad8f021b9c05.png) 


- **配置合适的scope**
搜索/替换、Inspect时选择scope，排除不需要的文件（第三方库、非代码文件）。
 ![图片](https://dn-coding-net-production-pp.qbox.me/d737685a-4604-46b9-a09c-90881cfb9b90.png) 


- **配置合适的Inspections**
 ![图片](https://dn-coding-net-production-pp.qbox.me/fae554e7-9412-41f7-9b78-aa6a2b553311.png) 


- **配置开发部署服务器帐号**
 ![图片](https://dn-coding-net-production-pp.qbox.me/20a9bbcd-2673-4664-b40e-6eb70084946c.png) 


- **SQL方言正确选择**
 ![图片](https://dn-coding-net-production-pp.qbox.me/cff450e1-3a37-46d8-886c-66f993de541f.png) 


- **提交代码时的配置**
 ![图片](https://dn-coding-net-production-pp.qbox.me/974cb4d0-2d3f-4f3a-97f2-17bf39f314c6.png) 



## 导入配置
- baobaobooks工程根目录下有`ps-scope.txt`，通过`Preference | Appearance & Behavior | Scopes`新建scope "php"，粘贴`ps-scope.txt`到`Pattern`。
- 参考[Sharing Your IDE Settings](https://www.jetbrains.com/help/phpstorm/2016.3/sharing-your-ide-settings.html)，通过git共享setting 。 **如果你的setting有更新并且适合共享给大家，请Overwrite Remote。**
 ![图片](https://dn-coding-net-production-pp.qbox.me/a4aaa57b-6e2d-41d4-ac96-6b69dc3ba743.png) 


- 不可共享的配置（Inspections虽然有icon，实际可共享）
 ![图片](https://dn-coding-net-production-pp.qbox.me/18ed5f22-21f7-4d4d-bd2f-0042d77183e3.png) 



##  常用快捷键（Windows）

**查看所有快捷键：Help - Keymap Reference**


快捷键                        | 功能
:-----------                 | :-----------
**Editing**                 |
Ctrl + Space                 | 基本代码完成(任意类的，方法的或者变量的名称)
Ctrl + Shift + Enter         | 补全当前语句
Ctrl + P                     | 参数信息 
Ctrl + Q                     | 快速查找文档
Ctrl + 鼠标滑过              | 简明信息查看
Ctrl + F1                    | 在插入符号处显示错误或者警告信息
Alt + Insert                 | 生成代码...(Getters,Setters,Constructors)
Ctrl + O                     | 重写方法
Ctrl + I                     | 实现方法
Ctrl + Alt + T               | 使用if...else,try...catch,for等包围代码
Ctrl + /                     | 注释/取消行注释
Ctrl + Shift + /             | 注释/取消块注释
Ctrl + W                     | 增量式选择代码
Ctrl + Shift + W             | 减少选择的代码块，与Ctrl+W相反
Alt + Q                      | 上下文信息
Alt + Enter                  | Show	intention	actions	and	quick-fixes
Ctrl + Alt + L               | 格式化代码
Ctrl + Alt + I               | 自动缩进单行或者多行
Tab/Shift + Tab              | 缩进选中的行或者取消选中行的缩进
Ctrl + X or Shift+Delete     | 剪切
Ctrl + C or Shift+Insert     | 复制
Ctrl + V or Shift+Insert     | 粘贴
Ctrl + Shift + V             | 从历史中粘贴
Ctrl + D                     | 复制当前的行或者选中的块  
Ctrl + Y                     | 在插入符号处删除行
Ctrl + Shift + J             | 合并行   
Ctrl + Enter                 | 拆分行   
Shift + Enter                | 新起一行
Ctrl + Shift + U             | 切换大小写
Ctrl + Shift + ]/[           | 选择代码块到开始或者结尾
Ctrl + Delete                | 删除单词从光标处到到结尾
Ctrl + Backspace             | 删除单词从光标处到开头
Ctrl + NumPad+/-             | 展开或者折叠代码块 
Ctrl + Shift +NumPad+        | 展开所有
Ctrl + Shift +NumPad-        | 折叠所有
Ctrl + F4                    | 关闭编辑页面
**Search/Replace**           | 
Ctrl + F                     | 查找
F3                           | 查找下一个
Shift + F3                   | 查找上一个
Ctrl + R                     | 替换
Ctrl + Shift + F             | Find in path 
Ctrl + Shift + R             | Replace in path
**Usage Search**             | 
Alt + F7/Ctrl + F7           | 查找使用处/在文件中查找使用处
Ctrl + Shift + F7            | 在文件中高亮使用处
Ctrl + Alt + F7              | 显示所有使用处
**Running**                  | 
Alt + Shift + F10            | 选择配置并运行
Alt + Shift+ F9              | 选择配置并调试
Shift + F10                  | 运行
Shift + F9                   | 调试
Ctrl + Shift + F10           | 从编辑器运行环境配置    
Ctrl + Shift + X             | 运行命令行
**Debugging**                | 
F8                           | 逐过程
F7                           | 逐语句
Shift + F7                   | 智能单步执行
Shift + F8                   | 跳出
Alt + F9                     | 运行到光标处
Alt + F8                     | 计算表达式
F9                           | 重新开始程序
Ctrl + F8                    | 切换断点
Ctrl + Shift + F8            | 查看所有断点
**Navigation**               | 
Ctrl + N                     | 查找类
Ctrl + Shift + N	         | 查找文件
Ctrl + Alt + Shift + N       | 查找符号
Alt + Right/Left             | 切换上一个/下一个编辑区
F12                          | 回到以前的工具窗口
Esc                          | 从工具窗口到编辑区
Shift + Esc                  | 隐藏当前使用的或上次使用的窗口
Ctrl + Shift + F4	         | 关闭打开的运行/消息/查找/...	对话框
Ctrl + G                     | 调整到指定行
Ctrl + E	                 | 打开最近使用的文件显示框
Ctrl + Alt + Left/Right      | 导航回退或者前进
Ctrl + Shift + Backspace     | 定位到最后编辑区
Alt + F1	                 | 选择当前文件或者符号在任意显示窗口中(例如：结构，项目等)
Ctrl + B or Ctrl + Click     | 调整到声明处
Ctrl + Alt + B               | 调整到实现
Ctrl + Shift + I	         | 查看定义(例如：查看函数具体实现)
Ctrl + Shift + B             | 调整到类型声明处
Ctrl + U                     | 跳到父类/超类
Alt + Up/Down                | 跳到上一个/下一个方法
Ctrl + ] / [                 | 移动到代码块的结束/开始
Ctrl + F12                   | 显示文件结构
Ctrl + H                     | 类型层次结构,例如类的继承
Ctrl + Shift + H             | 方法的层次结构
Ctrl + Alt + H               | 调用层次结构
F2 / Shift + F2              | 下一个/以前的突出显示错误
F4 / Ctrl + Enter            | 编辑源代码 / 查看源代码
Alt + Home                   | 显示导航栏
F11                          | 切换书签
Ctrl + F11                   | 用助记符切换书签
Ctrl + #[0-9]                | 转到编号书签
Shift + F11                  | 显示所有书签
**Refactoring**              | 
F5  Copy                     | 复制
F6  Move                     | 移动
Alt + Delete                 | 安全删除
Shift + F6                   | 重命名
Ctrl + Alt + N               | 嵌入变量
Ctrl + Alt + M               | 提取方法
Ctrl + Alt + V               | 提取变量
Ctrl + Alt + F               | 提取字段
Ctrl + Alt + C               | 提取常量
**VCS/Local History**        | 
Alt + BackQuote (`)          |  VCS快速弹出
Ctrl + K                     | 提交项目到VCS
Ctrl + T                     | 从VCS更新项目
Alt + Shift + C              | 查看最近更改
**General**                  | 
Ctrl + Shift + A             | 查找Action
Alt + #[0-9]                 | 打开相应的工具窗口
Ctrl + Shift + F12           | 最大化切换编辑器
Alt + Shift + F              | 添加到收藏夹
Alt + Shift + I	             | 检查当前文件与当前概要文件
Ctrl + BackQuote (`)         | 快速切换当前主题
Ctrl + Alt + S               | 打开设置对话框
Ctrl + Tab                   | 在标签和工具窗口间切换


##  常用快捷键（macOS）
**查看所有快捷键：Help-Keymap Reference**

快捷键 | 功能
:----------- | :-----------
**Editing** |
 ⌃Space  |**自动补齐** 
⌘/            | **//** 
⌥⌘/	| **/\*\*/** 
⌘N | **Generate code**（生成构造函数、重写函数、待实现函数、Getters、Setters、Copyright、PHPDoc）
⌥↑ and ⌥↓	|**扩大和缩小选中的范围**（字符串、代码作用域...）
⌘⌥L | **格式化代码** 
⌘D	        | **拷贝粘贴当前行或选中的代码** 
⌥⇧↑ / ⌥⇧↓	        | **Move Line Up / Down** 
⌘⇧↑ / ⌘⇧↓	        | **Move Statement Up / Down** 
⌘delete	        | **删除选中的代码** 
⇧⏎ | **当前行后开始新的一行** 
⌘⇧U | **切换选中字符的大小写** 
⌘+ / ⌘- | **打开或收起代码块** 
⌘⇧V | **从历史记录中粘贴** 
⌘L     | **跳转至某一行** 
⌘J	        | **插入代码模板** （echo, foreach...）
⌘+ / ⌘- | **打开或关闭代码块** 
⌥⏎ |提示可做的操作列表（出现错误或警告时可用）
⌘⌥T | 将选中的代码包裹 （{}、if、for、try catch、function）
**Search/Replace** |
⌘F / ⌘R	| **当前文件查找/替换** 
⌘⇧F / ⌘⇧R | **在全局或选中的文件路径查找/替换** 
⌘G / ⌘⇧G |  **查找下一个/上一个** 
**Usage Search** |
⌥F7 | **Find usages** 
⌘⌥F7 | **Show usages** 
⌘⇧F7 | **Highlight usages in file** 
**Refactoring** |
⌃T | **Refactor This**  (shows all available refactorings)
F5 / F6 | **Copy/Move** （文件、类、函数、变量...）
Shift F6 | **Rename** （文件、类、函数、变量...）
⌘delete | **safe Delete** 
**Running** |
⌃⇧R / ⌃⇧D | **运行当前文件代码** 
⌘⇧X | **运行控制台命令** 
**Navigation** |
⌥F1 | **Select In...** 
⌘B / ⌘+Click | **Declaration** 
⌘F12 | **File Structure** 
⌘L     | **跳转至某一行** 
⌘O / ⇧⌘O	| **打开类** 
⌘W      | **关闭当前Tab** 
⌥⌘→ / ⌥⌘← | **切换Tab** （修改为与Chrome一致）
⌘E | **Recent Files** 
⇧⌘E | **Recent Changed Files** 
⌘[ | **Back** 
⌘[ | **Forward** 
F2 | **Next Highlighted Error** 
⇧F2 | **Previous Highlighted Error** 
⌃⌥H | **Call hierarchy** 
**VCS/Local History** |
⌃V |**‘VCS’ quick popup** 
⌘K | **Commit** 
⌘T | **Update project** 
⌘⇧	        | **出现文件导航** （全屏编辑文件时有用）
⌘↓   	|新窗口编辑文件（=双击）
**General** |
⇧⇧ | **查找任何地方** （文件、工具栏、配置）
⌘, | **打开Preference** 
⌘N | **新建文件** 
⌘⇧X | **Upload To Default Server** （已修改）