---
layout: post
title: "Git Commands List"
date: 2017-05-13 11:41:06 +0800
description: 常用的Git命令集合，不断完善
tags: 
 - Git
---
## 常用指令
- `$git clone [url] [--depth=1]`　克隆远端分支到本地,--depth=1仅克隆最近因此的提交，加快速度 
- `$git config --list`　输出git的当前配置
-  `$git add [.]`　增加当前目录的所有变化文件到暂存区
- `$git commit -m [message]`　提交变化到本地仓库
- `$git branch`　列出所有本地分支
   - `-r`　远端分支
   - `-a`　远端分支和本地分支
- `$git push`　提交本地修改到远端分支
- `$git pull`　取回远端仓库的变化并与本地分支合并
- `$git checkout [branch name]`　切换到指定分支，同时更新工作区
- `$git status` 　显示所有的变更文件
- `$git log`　显示版本提交历史
- `$git reset --hard [commit]`　重置当前分支到指定的commit