---
title: 第二十四课：服务器可用性设计
date: 2021-04-22 15:01:00 +0800
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

# 第一章：服务器可用性的概念

## 可用性的概念和度量

系统在面对各种异常时可以提供正常服务的能力

正常服务业务和生存系统业务是不一样的，生存系统业务指一个服务的核心业务，如QQ的通信服务，播放器的播放服务，游戏的核心玩法。

**可用性的度量：**

![Screen Shot 2021-04-22 at 15.28.59](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.28.59.png)

## 可用性级别

略

## 影响可用性的因素

|          | 错误                                 | 灾难                                 |
| -------- | ------------------------------------ | ------------------------------------ |
| 分类     | 功能错误<br />进程宕机<br />硬件故障 | 系统故障<br />自然灾害<br />人为破坏 |
| 关注人   | 开发人员                             | 运维人员                             |
| 出现频率 | 频繁                                 | 小                                   |

灾难问题一般由运维人员关注，但需要软件开发人员提供解决方案

## 典型错误类型和影响范围

<img src="../assets/blog_res/.assets/Screen%20Shot%202021-04-22%20at%2015.32.02.png" alt="Screen Shot 2021-04-22 at 15.32.02" style="zoom: 50%;" />

# 第二章：容灾容错分级

<img src="../assets/blog_res/.assets/Screen%20Shot%202021-04-22%20at%2015.32.55.png" alt="Screen Shot 2021-04-22 at 15.32.55" style="zoom:50%;" />

## 进程容错

**错误隔离原理：**

服务器的两类驱动源是请求和定时器，对逻辑错误的隔离可以转化为对引起的错误的请求和定时器的隔离。

**错误隔离系统的设计：**

![Screen Shot 2021-04-22 at 15.34.34](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.34.34.png)

## 进程容灾

引起进程宕机的原因：

- 代码Bug ：空指针、越界……
- 系统限制：堆栈溢出、内存溢出
- 人为因素：运维误操作、死循环强杀

**一种朴素的状态维护方式**

![Screen Shot 2021-04-22 at 15.36.54](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.36.54.png)

不适合强交互类游戏，IO过多



**使用共享内存维护状态：**

如果不调用shmdt，进程推出后shm仍然保存在内核中。进程重新启动后重新shmat这块内存的技术我们称之为resume

**共享内存数据的组织形式：**

- 大小固定、数量固定，使用对象池比使用内存池更好～

## 系统容灾

**单点：**

- 系统中只存在唯一实例的节点
- 单点是获取/维护某些值（决议）的权威方
- 关键路径单点/非关键路径单点

**针对单点问题的应对策略：**

![Screen Shot 2021-04-22 at 15.41.04](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.41.04.png)

1. 冗余部署：增加链路、增加备份节点，适用无状态或者弱状态进程

使用主从服务器集群，用zookeeper，它有一个选择算法让一个成为主节点。

### 主从数据同步：逻辑同构

![Screen Shot 2021-04-22 at 15.43.15](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.43.15.png)

### 主从数据同步：版本号机制

![Screen Shot 2021-04-22 at 15.43.49](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.43.49.png)

### 主从数据同步：定时快照

![Screen Shot 2021-04-22 at 15.44.38](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.44.38.png)

## 数据容灾

数据分类：

1. 游戏数据
2. 用户流水（非常重要，用户的每个操作，将来是要回溯的）
3. 系统状态
4. 进程日志

![Screen Shot 2021-04-22 at 15.46.01](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.46.01.png)

总结：

![Screen Shot 2021-04-22 at 15.46.27](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.46.27.png)

在线热备：

![Screen Shot 2021-04-22 at 15.46.41](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.46.41.png)

定时备份+流水

![Screen Shot 2021-04-22 at 15.47.05](../assets/blog_res/2021-04-22-fu-wu-qi-ke-yong-xing-she-ji.assets/Screen%20Shot%202021-04-22%20at%2015.47.05.png)