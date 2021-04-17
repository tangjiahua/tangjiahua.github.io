---
title: 第十二课：核心系统设计——服务器地形
date: 2021-04-18 01:55:00 +0800
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

# 服务器地形管理基础概念

**地形：**山川河流路面等等

**为什么要有地形管理？**

- 用数据描述地形信息
- 组织高度，阻挡信息
- 提供玩家定位访问、信息访问机制
- 为上层模块提供定位服务

**服务器如何描述地形数据？**

- 2D游戏
  - grid网格
  - 无高度信息，只有阻挡信息
- 3D游戏
  - 3D地形场景

# 服务器地形管理实践

**2D的实现方式：**

- Grid Mask网格
  - 二维数组，（x，y）判断位置
  - 获取grid信息是用的mask特征

**3D的实现方式：**

- Grid Layer网格
  - 三位数组，新增layer一层
  - Grid Mask网格的扩展
  - (x,y,z,layer)三元组描述对象位置
  - 可以保留mask特征
  - **问题在于：旋转楼梯的复杂地形，导致layer网格出现悖论**

- Voxel Grid
  - 体素网格
  - 描述能力强
  - 服务器随机访问性能较高
  - 数据结构简单，代码可维护性强
  - <img src="/assets/blog_res/2021-04-18-fu-wu-qi-di-xing.assets/Screen%20Shot%202021-04-18%20at%2002.11.45.png" alt="Screen Shot 2021-04-18 at 02.11.45" style="zoom:35%;" align='left'/>

**服务器端地形管理的常见实现：**

- Mask Grid
- Mask Grid Layer
- Polygon Mesh
- Voxel Grid