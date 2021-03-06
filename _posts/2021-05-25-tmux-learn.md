---
title: Tmux & iTerm2
date: 2021-05-25 00:11:00 +0800
categories: [Unix网络编程]
tags: [技术]
pin: true
author: Tang Jiahua

toc: true
comments: true
Typora-root-url: ..
math: false
mermaid: true
---

# iTerm2 + Tmux结合的操作方法

创建新的Window：tmux ls && read session && tmux -CC attach -t ${session:-default} \
|| tmux -CC new -s ${session:-default}

tmux -CC 后面跟上的命令都和一般的tmux相同

Command+Shift+W可以直接快速detach当前的session

(Command+Control+A是快捷键，一般设置为快速打开一个新的Session窗口)

# iTerm2

- 切换 tab：⌘+←, ⌘+→, ⌘+{, ⌘+}。⌘+数字直接定位到该 tab；
- 新建 tab：⌘+t；
- 切分屏幕：⌘+d 水平切分，⌘+Shift+d 垂直切分；
- 智能查找，支持正则查找：⌘+f。
- 列出曾经使用过的命令：⌘+;
- 使用历史记录：⌘+Shift+h

# Tmux

```shell
tmux new -s <name>	// 新建会话
tmux detach	// 退出tmux窗口
tmux ls	// 列出所有会话
tmux attach -t <name>	// 接入某个会话
tmux kill-session -t <name>	//	杀死会话
tmux switch -t <name>	//	切换会话
tmux rename-session -t 0 <name>	//	重命名会话


```

通过前缀键来命令

```shell

// 关于会话
Ctrl+b d //	分离当前会话detach
Ctrl+b s	//	列出所有会话并切换
Ctrl+b $	//	重命名当前会话
Ctrl+b :kill-session	// kill session


// 关于窗口
Ctrl+b c：创建一个新窗口，状态栏会显示多个窗口的信息。
Ctrl+b p：切换到上一个窗口（按照状态栏上的顺序）。
Ctrl+b n：切换到下一个窗口。
Ctrl+b <number>：切换到指定编号的窗口，其中的<number>是状态栏上的窗口编号。
Ctrl+b w：从列表中选择窗口。
Ctrl+b ,：窗口重命名。
Ctrl+d	:关闭窗口


// 关于窗格
Ctrl+b %：划分左右两个窗格。
Ctrl+b "：划分上下两个窗格。
Ctrl+b <arrow key>：光标切换到其他窗格。<arrow key>是指向要切换到的窗格的方向键，比如切换到下方窗格，就按方向键↓。
Ctrl+b x：关闭当前窗格。
Ctrl+b !：将当前窗格拆分为一个独立窗口。
Ctrl+b z：当前窗格全屏显示，再使用一次会变回原来大小。
Ctrl+方向键	以1个单元格为单位移动边缘以调整当前面板大小
Alt+方向键	以5个单元格为单位移动边缘以调整当前面板大小


```



其实不用开那么多shell，可以把不需要交互的作业放后台。

在bash中输入一条命令的时候，一般都是直接在前台完成。但有一些比较费时的命令，就需要放到后台中去运行，在命令行末尾加上&符号，命令就会在后台运行，切换到后台运行的进程都会被分配一个作业ID号。另外可以按下“CTRL+z”将当前前台运行的作业挂起到后台，再利用“bg”命令使其在后台恢复运行。

关于作业控制可以参考手册。