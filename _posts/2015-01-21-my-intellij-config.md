---
layout: post
title:  "我的IntelliJ配置"
date:   2015-01-21 09:24:00
categories: usenotes
---

本文在
![tested](https://img.shields.io/badge/IntelliJ-Communitiy_Edition_14-brightgreen.svg),
![tested](https://img.shields.io/badge/PyCharm-Communitiy_Edition_4-brightgreen.svg)
上通过了验证

![tested](https://img.shields.io/badge/Tested_on-Mac_OS_X_10.10-green.svg)

# 修改IntelliJ同步代理设置
---

FIXME...

# 修改IntelliJ的快捷键
---

打开IntelliJ -> Preferences对话框(或直接敲 `⌘,`), 直接搜索keymap或者选择以下路径: **Apprearance & Behavior** -> **Keymap**, 选择一个内置配置, 比如Eclipse (Max OS X). 搜索和修改以下映射值:

| 快捷键 | 用途 | 配置文件中ID | 我设置的键组合|
| :--- | :--- | :--- | :--- |
| Navigate: Back | 回到上一编辑位置 | Back | `⌘[` 或者 `⌘←` |
| Navigate: Forward | 回到继续编辑的位置 | Forward | `⌘]` 或者 `⌘➞` |
| Refactor: Rename | 重命名类/文件等 | RenameElement | `⌘R` |
| Find Usages | 查找被引用的地方 | FindUsages | `⌘U` |
| Jump to Source | 跳转到定义处 | EditSource | `⌘+单击` 或者 `⌘I` |

* 拷贝快捷键配置文件到其他Jetbrains产品

IntelliJ Community Edition 14所在的快捷键配置文件路径:

**~/Library/Preferences/IdeaIC14/keymaps/**

在~/Library/Preferences/你可以发现其他基于Idea平台的产品,比如AndroidStudio, PyCharm等等, 可以直接从上述目录中拷贝配置文件到其它产品下, 就省下重新设置快捷键的麻烦.

以下表格是我统计的Jetbrains的各产品名称和路径缩写的映射关系:

| 产品 | 适用的版本 | 路径名前缀 |
| :--- | :--- | :--- |
| IntelliJ | 13, 14 | IntelliJIdea |
| IntelliJ Community Edition | 13, 14 | IdeaIC |
| PyCharm | 4 | PyCharm |

