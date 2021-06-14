---
title: 鸟哥的Linux私房菜笔记
date: 2021-04-06 01:40:00 +0800
categories: [基础技术]
tags: [技术]
pin: true
author: Tang Jiahua

toc: true
comments: true
Typora-root-url: ..
math: false
mermaid: true



---

# 重点回顾

## 0x01

- 计算机的五大单元：输入单元、输出单元、控制单元、算术逻辑单元、存储单元，其中CPU占有算术逻辑单元和控制单元，存储单元包含内存和辅助内存；
- CPU设计理念依据RISC精简指令集和CISC复杂指令集；
- CPU频率：外频是CPU与外部元件进行数据传输时的速度，倍频是CPU内部用来加速工作性能的一个倍数，两者承积才是CPI的频率；
- 个人电脑的内存主要元件为DRAM，CPU内部的第二层高速缓存则使用SRAM；
- 目前主流的外接卡接口为PCIe接口；
- 磁盘连接到主板的接口大多为SATA或者SAS，台式机主流为SATA 3.0；

## 0x02

- 操作系统功能：管理与驱动硬件，管理内存、管理设备、负责进程管理、系统调用；
- Unix的前身是贝尔实验室的Ken Thompson利用汇编语言写成的，后来在1971-1973年间由Dennis Ritchie以C语言进行改写，才称为Unix；
- 1977年由Bill Joy放出BSD（Berkeley Software Distribution），这些称为Unix-like的操作系统；
- 1984年由Andrew Tanenbaum开始制作Minix操作系统，该系统可以提供源代码以及软件；
- 1984年由Richard Stallman提倡GNU（GNU's Not Unix），倡导自由软件（Free software），强调其软件可以“自由的获取、复制、修改和在发行”，并规范出GPL（GNU Public License）授权模式，任何GPL软件不可以单纯仅贩卖软件，也不可以修改软件授权；
- 1991年Linus Torvalds开发出Linux操作系统玩具，他基于Minix，GNU，Internet，POSIX以及虚拟团队开发出的后来为我们所知的Linux；
- 符合open source理念的授权有Apache/BSD/GPL/MIT等；
- Linux kernel 3.0开始，舍弃奇数和偶数的核心版本规划，新的规划使用主线版本为依据，提供长期版本支持来加强某些功能的持续维护；
- Linux distributions的组成：“Linux kernel + free software + documentations(tools) + 可完整安装的程序”所制成的一套完整的系统；
- 常见的Linux distributions有商业、社区分类，也有rpm、dpkg分类；

## 0x03

- linux每个设备都是一个文件，每个设备都有设备文件名，在/dev下；
- 硬盘设备文件名通常分为两种，实际SATA/USB名为/dev/sd[a-p]，而虚拟的设备可能为/dev/vd[a-p]；
- 磁盘第一个扇区主要记录了两个重要信息：（1）主要开机记录区（master boot record , MBR）：可以安装开机管理程序的地方，有446bytes；（2）分区表（partition table）：记录整个硬盘分区的状态，有64bytes；
- 磁盘的MBR分区方式中，主要与延伸分区最多可以有4个，逻辑分区的设备文件名号码一定从5号开始；
- 如果磁盘容量大雨2TB，系统自动使用GPT分区来处理磁盘分区；
- GPT分区已经没有延伸与逻辑分区的概念，可以想象所有分区都是主分区；
- 某些操作系统要使用GPT分区时，必须搭配UEFI的新型BIOS格式才可以安装使用；
- 开机流程：BIOS->MBR->->boot loader->核心文件；
- boot loader功能：提供菜单、载入核心、转角控制权给其他loader；
- boot loader可以安装的地点：MBR与boot sector；
- linux操作系统的文件使用目录树系统，与磁盘对应需要有挂载动作才行；
- 新手的简单分区，建议只要有/及swap两个分区即可。