---
layout: post
title: "Linux Commands"
date: 2017-05-10 11:41:06 +0800
description: 常用的linux命令集合，不断完善
tags: 
 - Linux
---
## 1.常用指令
- su　user/root　　切换用户 
- ls　显示文件或目录
   - -l　显示文件的详细信息
   - -a　显示隐藏的文件或目录
- cd　目录切换
- mkdir　创建目录
- echo　结果输出，可写入到文件
- touch　创建一个空的文件
- cat　查看文件内容
- cp　复制
- mv　移动
- rm　删除文件
  - -r　递归删除
  - -f　强制删除
- ln　创建链接
   - -s　创建软链接
- ctrl + alt + F1　切换到命令行模式
    - +alt + F2　切换到图形界面
- kill　杀死进程
- ps/top　查看进程id
- shutdown　关机
- reboot　重启

## 2.vim命令
- i　切换插入模式
- esc　切换到命令模式
命令模式下：
- :q　退出
- :w　写入
- :q!　强制退出
- :wq　保存后退出 