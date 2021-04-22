---
title: 第二十课：游戏开发中的数据表示
date: 2021-04-22 12:22:00 +0800
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

# 第一章：数据表示基础

## 导语

不同的语言、不同的编译架构、处理器架构导致了不同环境下的数据表示可能出现问题。因此我们需要一个DR System来作为中间层，它是异构系统间通信的桥梁，保证双方的数据表示是相同的。

## 什么是数据表示

- 数据表示
  - Data Representation(DR for short)
- 什么是数据
  - Data are the facts or  details from which information is derived
- 如何表示数据
  - Various forms for same information
  - for example <666>
- 数据表示的定义
  - DP is a group of methods taht can describe, reveal, and operate on information

## 数据表示的要素

- IDL - 接口描述语言
  - Interface Description Language
  - IDL是用来描述软件组件接口的一种计算机语言。IDL通过一种中立的方式来描述接口，使得在不同平台上运行的对象和用不同语言编写的程序可以相互通信交流。
- Data Operation - 数据操作支持
  - serialize / deserialize / visualize / transform / compression
- Version Control - 版本控制支持
  - 数据可以有不同版本，且版本之间可以按照一定规则兼容

## 业界现状

- Google - Protobug
- Apache Thrift Binary Protocol
- Tencent Data Representation

<img src="/assets/blog_res/2021-04-22-shu-ju-biao-shi.assets/Screen%20Shot%202021-04-22%20at%2013.00.21.png" alt="Screen Shot 2021-04-22 at 13.00.21" style="zoom: 67%;" />

## Protobuf In Action

![Screen Shot 2021-04-22 at 13.00.53](/assets/blog_res/2021-04-22-shu-ju-biao-shi.assets/Screen%20Shot%202021-04-22%20at%2013.00.53.png)

# 第二章：数据表示在游戏开发中的应用

## 游戏开发中的协议定义与管理

**痛点：**

- 游戏协议交互内容复杂：多重嵌套结构体/二进制数据
- 协议数量巨大：4000+条协议定义，13000+结构体定义
- 变更频繁：Average 1.6 modification/day
- 网络流量巨大：单机峰值流量超过600mbps

![Screen Shot 2021-04-22 at 13.04.12](/assets/blog_res/2021-04-22-shu-ju-biao-shi.assets/Screen%20Shot%202021-04-22%20at%2013.04.12.png)

## 异构系统协议交互

多设备，移动设备+PC+Console

## 协议版本兼容

- 快速迭代下的版本控制
  - 通过DR提供的版本控制来进行协议兼容

通过optional可以保证服务器能处理老版本的客户端协议发来的数据

## 协议流量优化

通过DR提供的数据压缩功能进行流量优化

## 游戏开发中的数据存储

- 游戏开发中数据存储的特点
  - 数据结构复杂：每个玩家的存储设计到成千上万个字段
  - 数据结构不稳定：每次版本更新有可能会新增字段或扩大原有字段
  - Update > read > insert > delete

## 游戏中数据存储的特点

传统范式设计

- 表格多且巨大难以维护
- 大量连表查询，效率低下
- 数据结构变更困难：对已经存在的大量数据的表格做alter操作新增列耗时巨大

## 游戏数据存储设计与管理

- KV数据存储模型
  - key - 角色id
  - value - 二进制角色数据
  - maysql Blob
- 使用DR管理Blob数据
  - 数据序列化/反序列化
  - 数据兼容
  - 数据压缩

<img src="/assets/blog_res/2021-04-22-shu-ju-biao-shi.assets/Screen%20Shot%202021-04-22%20at%2013.11.03.png" alt="Screen Shot 2021-04-22 at 13.11.03" style="zoom:67%;" />