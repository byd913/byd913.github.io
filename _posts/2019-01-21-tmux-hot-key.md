---
layout: post
title:  "tmux常用快捷键"
date:   2019-01-21 14:00:00
categories: Linux
tags: Linux, tmux, hot key
author: LuckyBoy
location: Beijing, China
description: tmux常用快捷键记录
---
---

# tmux 快捷键

prefix 为前置的按键，默认为`ctrl+b`，每次需要先按前置按键。下面分以下几类分别介绍

* session
* window
* panel
* 其他

# session

| 按键   | 操作的效果                                                     |
|--------|----------------------------------------------------------------|
| ?      | 列出所有的快捷键，按q返回                                      |
| d      | 脱离当前回话，输入tmux attach可以重新键入                      |
| r      | 强制重绘未脱离的回话                                           |
| s      | 选择并切换回话                                                 |
| :      | 进入命令行模式                                                 |
| [      | 进入复制模式，此时的操作为vim/emacs相同，按Enter复制选中的内容 |
| ctrl+c | 创建新的session                                                |
| $      | 重命名当前的session                                            |

# window

| 按键          | 操作的效果                   |
|---------------|------------------------------|
| c             | 创建新的窗口                 |
| &             | 关闭当前窗口                 |
| 数字键(0,1,2) | 切换至指定的窗口             |
| p             | 切换至上一个窗口             |
| n             | 切换至下一个窗口             |
| w             | 通过窗口列表选择切换窗口     |
| ,             | 重命名当前窗口               |
| .             | 修改当前窗口的编号           |
| f             | 在所有的窗口中查找指定的文本 |

# panel

| 按键          | 操作的效果                                |
|---------------|-------------------------------------------|
| "             | 将当前的面板平分为上下两个panel           |
| %             | 将当前的面板平分为左右两个panel           |
| x             | 关闭当前的panel                           |
| !             | 将当前的panel重置于一个新的window         |
| ctrl + 方向键 | 以一个单元格为单位移动调整当前panel的大小 |
| alt + 方向键  | 以五个单元格为单位移动调整当前panel的大小 |
| q             | 显示前panel的编号                         |
| o             | 在当前窗口选择下一个panel                 |
| 方向键        | 移动选择面板                              |
| {             | 向前置换当前面板                          |
| }             | 向后置换当前面板                          |

# 其他

* tmux attach -d：恢复并且attach到一个session
* tmux attach -t session_name 指定session的名称