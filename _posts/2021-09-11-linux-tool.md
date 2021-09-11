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



来源：https://linuxtools-rst.readthedocs.io/zh_CN/latest/base/03_text_processing.html

# Linux工具基础

## 命令帮助

- info command：显示工具的详细信息
- man command：显示工具的使用手册
- whatis command：显示工具的简介
- which command：显示工具的所在路径
- whereis command：显示工具的搜索路径（当系统中安装了同一个软件的多个版本，就可以用这个命令）

## 文件和目录管理

- ls -lrt：时间排序，-r是reverse，-t是时间排序
- cat：将文件或标准输入组合输出到标准输出。 这个命令常用来显示文件内容，或者将几个文件连接起来显示，或者从标准输入读取内容并显示，它常与重定向符号配合使用。
- find ./ -name "*.o"：查找目标文件夹是否含有文件
- tail -5 filename：显示文件倒数五行
- head -5 filename：显示文件正数五行
- diff file1 file2：显示文件差别
- chmod, chown, chgrp：修改权限，用得不是很多
- ln cc ccAgain：硬链接，删除一个，仍然能找到
- ln -s cc ccTo：软连接，符号链接，删除源，目标无法使用
- |：批处理命令连接执行
- ;：串联，使用分号
- &&：前面成功，则执行后面，否则不执行
- ||：前面失败，后面一条也执行

<img src="../../../UGit/opensource/tangjiahua.github.io/assets/blog_res/2021-09-11-linux-tool.assets/image-20210911212852411.png" alt="image-20210911212852411" style="zoom: 50%;" />

- \>和>>：重定向文件，\>会覆盖目标的原有内容。 当文件存在时会先删除原文件，再重新创建文件，然后把内容写入该文件；否则直接创建文件。>> 会在目标原有内容后追加内容。

- bash快捷键：

  - ```bash
    Ctl-U   删除光标到行首的所有字符,在某些设置下,删除全行
    Ctl-W   删除当前光标到前边的最近一个空格之间的字符
    Ctl-H   backspace,删除光标前边的字符
    Ctl-R   匹配最相近的一个文件，然后输出
    ```

    

    <img src="../../../UGit/opensource/tangjiahua.github.io/assets/blog_res/2021-09-11-linux-tool.assets/image-20210911213350124.png" alt="image-20210911213350124" style="zoom: 67%;" />

## 文本处理



## 磁盘管理

## 进程管理

## 性能监控

## 网络监控

## 用户管理

## 系统管理及IPC资源管理

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



