title: sublimetext个人习惯的快捷键设置
date: 2016-09-09 10:12:39
tags: "sublime text"
---
[
{ "keys": ["ctrl+d"], "command": "find_under_expand" },
// 删除一整行
{ "keys": ["super+d"], "command": "run_macro_file", "args": {"file": "Packages/Default/Delete Line.sublime-macro"} },
// 光标移动到下一行
{ "keys": ["shift+enter"], "command": "run_macro_file", "args": {"file": "Packages/Default/Add Line.sublime-macro"} },
// 当前行与前一行互换位置
{ "keys": ["super+up"], "command": "swap_line_up" },
// 当前行与下一行互换位置
{ "keys": ["super+down"], "command": "swap_line_down" }
]
