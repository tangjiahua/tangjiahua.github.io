---
title: 第六课：游戏人工智能
date: 2021-04-08 23:53:00 +0800
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

# 游戏人工智能综述

人工智能在游戏中的应用

- 赋能与效率
  - 游戏体验
  - 开发效率
- 应用领域
  - 玩游戏
  - 内容生成
  - 玩家体验衡量

# 人工智能在游戏制作中的主要方法

## 决策

### 有限状态机（FSM）

离散、有限的性质

![Screen Shot 2021-04-09 at 00.22.59](/assets/blog_res/2021-04-08-you-xi-ren-gong-zhi-neng.assets/Screen%20Shot%202021-04-09%20at%2000.22.59.png)

- 优点
  - 快速简单
  - 计算开销少
- 缺点
  - 状态过多的时候，难以维护

**改进方式：分层**

![Screen Shot 2021-04-09 at 00.24.04](/assets/blog_res/2021-04-08-you-xi-ren-gong-zhi-neng.assets/Screen%20Shot%202021-04-09%20at%2000.24.04.png)

大状态是战斗、休息，小状态是内部的一些状态。

### 行为树（Behavior Tree）

![Screen Shot 2021-04-09 at 00.26.39](/assets/blog_res/2021-04-08-you-xi-ren-gong-zhi-neng.assets/Screen%20Shot%202021-04-09%20at%2000.26.39.png)

- 优点
  - 逻辑结构清晰
  - 行为数据与逻辑分离
  - 可重用
  - 可视化方便修改
- 缺点
  - 遍历开销大
  - 过于抽象，节点颗粒度小

**改进方式：因为每一个节点执行成功或失败，后续节点的执行是固定的。根据成功或者是失败可以获得多个序列**

![Screen Shot 2021-04-09 at 00.34.26](/assets/blog_res/2021-04-08-you-xi-ren-gong-zhi-neng.assets/Screen%20Shot%202021-04-09%20at%2000.34.26.png)

行为树就可以更换为数组的形式，用数组的形式来走这个迭代树会更不错一些，比如在内存中就节省更多空间。

### GOAP

目标导向的决策方法

- Goal Oriented Action Planning
- GOAP：模块化
- FSM：复杂性依赖AI
- BehaviorTree：静态结构，不灵活

Goal：目标条件

Action：条件、效果、成本

Planner：择优规划满足目标的Action序列

![Screen Shot 2021-04-09 at 00.38.08](/assets/blog_res/2021-04-08-you-xi-ren-gong-zhi-neng.assets/Screen%20Shot%202021-04-09%20at%2000.38.08.png)

## 棋盘游戏AI

- 建模
  - 博弈树
  - 局面评估函数
  - 在当前状态找到最优分支

### MiniMax算法



### Alpha-Beta剪枝算法



### 蒙特卡洛算法



## 导航

### A*/IDA🌟

路径搜索算法就看[amitp的A*搜索算法概要](https://www.redblobgames.com/pathfinding/a-star/introduction.html)

### JPS



### NavMesh

recast生成导航网格

## 高阶技巧

### 智能优化算法——遗传算法

- 优点
  - 算法鲁棒性较强
  - 适用于所有赛道
- 缺点
  - 不能解决动态因子影响
  - 技巧建模复杂
- 改进方向
  - 监督学习
    - 利用玩家的录像训练模型，学习玩家跑法
  - 强化学习
    - AI反复跑图进化

### 监督学习

- 高阶技巧不会使用（高阶技巧的样本在整个赛道中的占比很少）
- 高手样本占比大，缺少异常样本（加入低水平样本，会拉低整体水平）
- 复杂地图训练难度大（各种不同类型路段的地图）
- 需要介入额外辅助程序（异常检测、复位）

### 强化学习

![Screen Shot 2021-04-09 at 15.46.09](/assets/blog_res/2021-04-08-you-xi-ren-gong-zhi-neng.assets/Screen%20Shot%202021-04-09%20at%2015.46.09.png)



# 人工智能在游戏制作中的具体应用



# 人工智能在游戏运营中的应用实践

![Screen Shot 2021-04-09 at 16.17.21](/assets/blog_res/2021-04-08-you-xi-ren-gong-zhi-neng.assets/Screen%20Shot%202021-04-09%20at%2016.17.21.png)

- 抽取式与生成式的文本摘要