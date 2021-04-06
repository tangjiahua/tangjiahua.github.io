---
title: 浅谈游戏后台开发+游戏技术人员的野望
date: 2021-04-06 22:20:00 +0800
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

# 游戏后台解决的三大问题

- 网络通信
- 仲裁计算
- 数据存储

# Books

- C++编程思想
- Effective C++
- Unix网络编程（卷1:套接字联网API）
- UNIX环境高级编程
- TCP/IP详解
- 设计模式：可复用面向对象软件的基础
- 重构：改善既有代码的设计

# 游戏后台涉及的技术

- 同步方案
  - 帧同步（王者荣耀移动）
  - 状态同步
- 不同运营商之间的通信层处理
  - 加速软件
  - 服务器使用三块网卡同时接入三个运营商
  - 网络状态切换（WiFi到4G）

# 游戏后台的核心技术

- 通信
  - TCP、UDP、HTTP
  - 协议格式、流量、包量
  - 长连接、短连接
  - 加密解密，压缩
  - 弱网、断线重连
  - 网络同步
- 计算
  - 架构
  - 反外挂
  - 统计监控、安全校验
- 存储
  - sql
  - 数据一致性、CAP原则
  - 实时性
  - 数据修改

# 游戏后台架构

分区分服和全区全服

![Screen Shot 2021-04-06 at 23.35.43](/assets/blog_res/2021-04-06-qiantanyouxihoutaikaifa.assets/Screen%20Shot%202021-04-06%20at%2023.35.43.png)

