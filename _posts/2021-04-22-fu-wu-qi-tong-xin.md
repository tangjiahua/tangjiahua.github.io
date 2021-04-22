---
title: 第十七课：核心逻辑设计——战斗系统进阶
date: 2021-04-21 16:37:00 +0800
categories: [腾讯游戏学院]
tags: [技术]
pin: true
author: Tang Jiahua

toc: true
comments: true
Typora-root-url: ..
math: false
mermaid: true


---

# 第一章：概述

## 从实例介绍网络通信的基础知识

略，计算机网络课有大把的基础知识

# 第二章：CS通信

## 网络通信的基本过程

- TCP：可靠、适合大数据量、频繁交互的
- UDP：可靠性要求不高、小数据量、性能更佳

通过对UDP再应用层的处理其实可以保证可靠。

## 传输协议及应用实例

- PC上QQ的CS交互
  - 一般情况：UDP
  - 网络差：TCP
  - 拉取大文件如图片：TCP
- 手机上微信的CS交互
  - 前台：TCP长连接
  - 后台：TCP短连接
  - 查看文章等：HTTP（TCP短连接）

![Screen Shot 2021-04-22 at 11.05.47](../assets/blog_res/2021-04-22-fu-wu-qi-tong-xin.assets/Screen%20Shot%202021-04-22%20at%2011.05.47.png)

## 常见问题及优化

**设计CS交互的一些问题：**

![Screen Shot 2021-04-22 at 11.10.39](../assets/blog_res/2021-04-22-fu-wu-qi-tong-xin.assets/Screen%20Shot%202021-04-22%20at%2011.10.39.png)

**其他要点：**

- 非阻塞IO：O_NONBLOCK
- 多路复用：select, poll, epoll

# 第三章：SS通信

## 服务器间的常见通信方式

- TCP：最常用
- UDP：非关键数据上报、日志服务
- 非socket通信：PIPE, SIGNAL, SHM, MESSAGE QUEUE, FILE

## 服务器通信会遇到的问题

略