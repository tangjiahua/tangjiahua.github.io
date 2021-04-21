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

### buff系统

- 依附于实体数据上持续一段时间的可交互对象
  - 数据
  - 逻辑
  - 相关实体
    - event_source, event_target, deco_source
  - 交互点
    - SkillOut
    - SkillIn

Buff是挂在在player身上的，也就是每个player对象身上是有个链表挂着Buff的数据。

![Screen Shot 2021-04-21 at 15.51.23](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-ji-chu.assets/Screen%20Shot%202021-04-21%20at%2015.51.23.png)

#### 简单实现实例

**魔法盾的实现：**

- 玩家给自身上一个魔法盾的buff，在buff持续期间，任何HP上海都会被转换成MP上海
- 实现方式：在Skillin阶段，将所有的HP伤害Effect转换为MP伤害Effect
- Buff：就是target身上的一块数据，其中有个skill_in阶段，挂一个函数（从资源文件加载），把伤害type从hp改为mp

**Cooperator和目标扫描：**

![Screen Shot 2021-04-21 at 15.54.50](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-ji-chu.assets/Screen%20Shot%202021-04-21%20at%2015.54.50.png)

目标扫描：通过对玩家所在区域附近的玩家进行筛选，选择附近的玩家。

技能发动：由于目标扫描+buff遍历，因此每一次释放aoe技能都会导致O(n^2)的复杂度。

### 修饰系统

<img src="/assets/blog_res/2021-04-21-zhan-dou-xi-tong-ji-chu.assets/Screen%20Shot%202021-04-21%20at%2016.31.15.png" alt="Screen Shot 2021-04-21 at 16.31.15" style="zoom:67%;" />

# 逻辑内容

## 基本实现方式

- 可编译代码（服务器程序员）：C/C++
- 可配置脚本资源文件（策划）：Lua，expression

## 逻辑内容方案选择

- 第三方脚本语言：如Lua
  - 初次开发工作量较少
  - 后续运行时操作复杂度高
- C语言自己实现：expression
  - 需要开发一套脚本执行管理系统
  - 后续运行时操作复杂度较低（动态修改执行内容以及性能优化）

**Expression配置实例：**

![Screen Shot 2021-04-21 at 16.34.40](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-ji-chu.assets/Screen%20Shot%202021-04-21%20at%2016.34.40.png)

动态执行配置文件里面的脚本代码



附录：战斗系统在整体架构中的位置：

![Screen Shot 2021-04-21 at 16.35.12](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-ji-chu.assets/Screen%20Shot%202021-04-21%20at%2016.35.12.png)