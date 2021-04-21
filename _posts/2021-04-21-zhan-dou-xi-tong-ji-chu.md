---
title: 第十六课：核心逻辑设计——战斗系统基础
date: 2021-04-21 10:58:00 +0800
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

# 游戏战斗系统核心抽象模型

## 什么是战斗系统

- 客户端：负责接收玩家战斗指令，根据服务器的驱动进行表现
- 服务器：负责逻辑驱动

## 技能基本框架

- 技能过程定义
  - 技能实体在生命过程中，可以通过抽象划分为一系列的阶段
  - 不同的技能类型即为这些阶段组合而成的过程
- 技能阶段
  - Start - 技能开始
  - Cost - 消耗处理
  - Reading - 吟唱
  - Channeling - 引导
  - OnCast - 出手
  - Project - 弹道飞行中
  - OnHit - 击中
  - Finish - 一个技能结束

**简单的技能流程：**

![Screen Shot 2021-04-21 at 11.10.23](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-ji-chu.assets/Screen%20Shot%202021-04-21%20at%2011.10.23.png)

## 简单实现方式

![Screen Shot 2021-04-21 at 11.11.01](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-ji-chu.assets/Screen%20Shot%202021-04-21%20at%2011.11.01.png)

# 核心框架

## 战斗框架子系统



## 简单实现实例

# 逻辑内容

## 基本实现方式

## 逻辑内容方案选择