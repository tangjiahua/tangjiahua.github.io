---
title: 《Tmux命令》
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
Ctrl+b d //	分离当前会话detach
Ctrl+b s	//	列出所有会话并切换
Ctrl+b $	//	重命名当前会话
Ctrl+b %：划分左右两个窗格。
Ctrl+b "：划分上下两个窗格。
Ctrl+b <arrow key>：光标切换到其他窗格。<arrow key>是指向要切换到的窗格的方向键，比如切换到下方窗格，就按方向键↓。
Ctrl+b x：关闭当前窗格。
Ctrl+b !：将当前窗格拆分为一个独立窗口。
Ctrl+b z：当前窗格全屏显示，再使用一次会变回原来大小。


// 窗口快捷键
Ctrl+b c：创建一个新窗口，状态栏会显示多个窗口的信息。
Ctrl+b p：切换到上一个窗口（按照状态栏上的顺序）。
Ctrl+b n：切换到下一个窗口。
Ctrl+b <number>：切换到指定编号的窗口，其中的<number>是状态栏上的窗口编号。
Ctrl+b w：从列表中选择窗口。
Ctrl+b ,：窗口重命名。
```

