---
title: linux工具
date: 2021-09-11 00:11:00 +0800
categories: [Linux]
tags: [技术]
pin: true
author: Tang Jiahua

toc: true
comments: true
Typora-root-url: ..
math: false
mermaid: true
---

# Linux工具基础

- info command：显示工具的详细信息
- man command：显示工具的使用手册
- whatis command：显示工具的简介
- 

# Linux工具进阶

# Linux工具参考

## gdb调试工具

### gdb交互命令

#### 运行

- r：run, 运行程序直到遇到断点处停止运行，等待用户输入下一步的命令
- c：continue, 继续运行，到下一个断点处
- n：next, 单步跟踪程序，遇到函数不会进入函数体
- s：step, 单布调试，遇到了函数要进入函数
- u：until, 运行程序直到退出循环体
- u+行号：运行到某行
- finish：运行程序，直到当前函数完成返回，并打印函数返回时的堆栈地址呵呵返回值及参数值
- call 函数（参数）：调用程序中的可见函数，并 传递参数，如call gdb_test(55)
- q：quit，退出gdb

#### 设置断点

- b n：break n也可以，在第n行设置断点。可以带上代码路径和代码名称，如 b hello.cpp:21
- b fn1 if a > b：条件断点设置
- b func：在函数func的入口处设置断点，如break cb_button
- delete 断点号n：删除断点n
- disable n
- enable n
- clear n
- info b：等于info breakpoints，显示当前程序的断点设置情况
- delete breakpoints：清除所有的断点

#### 查看源代码

- l：list，默认显示10行源代码
- list 行号：将显示以行号为中心的前后10行代码
- list 函数名：显示函数的源代码
- list：将接着上一次list命令输出下面的内容

#### 打印表达式

- p 表达式：打印表达式内容
- display 表达式：在每次单步运行指令后，紧接着输出被设置的表达式及对应的值
- watch 表达式：设置一个监视点，若被监视的表达式值发生了改变，gdb将强行终止正在调试的程序
- whatis：查询变量或函数
- info function：查询函数
- info locals：显示当前堆栈页的所有变量

#### 查询运行信息

- where/bt：当前运行的堆栈列表
- bt：显示当前调用堆栈
- up/down：改变堆栈显示深度
- set args 参数：指定运行的参数
- show args：查看设置好的参数
- info program：查看程序是否在运行，进程号，被暂停的原因



