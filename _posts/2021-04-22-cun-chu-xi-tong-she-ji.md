---
title: 第二十一课：游戏服务器存储系统设计
date: 2021-04-22 13:15:00 +0800
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

# 第一章：数据存储基础

## 什么是数据存储



## 数据存储管理 & 数据库系统介绍

## 关系型数据库介绍

- 优点
  - 减少数据冗余（满足范式的基础）
  - 保证数据完整性
  - SQL语言提供了强大的查询功能
- 问题
  - 数据结构复杂情况下表结构难以维护
  - 性能一般，容易产生性能瓶颈
  - 可扩展性较差

## NOSQL数据库介绍

- 优点
  - 易于维护
  - 性能高
  - 可扩展性好
- 问题
  - 容易产生数据冗余
  - 不支持SQL查询

# 第二章：游戏服务器架构与数据存储设计

## 游戏业务的特点

- 响应速度要求高
  - 100ms以上的延迟玩家就会有感知
- 数据更新频率高
  - 玩家数据每时每刻都在变化
  - 获取经验，获取金钱，获得成就
  - update > read > insert > delete
- 解决方案
  - 为了实现高速响应，玩家数据全部在内存中
  - 在登录时从DB加载进内存
  - 游戏过程中的数据变更通过操作内存数据完成

## 游戏服务器架构介绍

分区分服：魔兽、天刀

全区全服：王者、PUBG

## 游戏服务器数据库选型

- 分区分服存储特点
  - 单服数据量较少
  - 请求量少
  - 无需动态在线扩容
  - RDBM
- 全区全服存储特点
  - 数据量大
  - 请求量大
  - 需要动态在线扩容
  - NOSQL

## 使用Mysql作为游戏数据库

![Screen Shot 2021-04-22 at 13.24.04](/assets/blog_res/2021-04-22-cun-chu-xi-tong-she-ji.assets/Screen%20Shot%202021-04-22%20at%2013.24.04.png)

## 游戏服务器存盘策略设计

![Screen Shot 2021-04-22 at 13.26.13](/assets/blog_res/2021-04-22-cun-chu-xi-tong-she-ji.assets/Screen%20Shot%202021-04-22%20at%2013.26.13.png)

## 游戏服务器存储容灾介绍

![Screen Shot 2021-04-22 at 13.26.43](/assets/blog_res/2021-04-22-cun-chu-xi-tong-she-ji.assets/Screen%20Shot%202021-04-22%20at%2013.26.43.png)

![Screen Shot 2021-04-22 at 13.27.05](/assets/blog_res/2021-04-22-cun-chu-xi-tong-she-ji.assets/Screen%20Shot%202021-04-22%20at%2013.27.05.png)