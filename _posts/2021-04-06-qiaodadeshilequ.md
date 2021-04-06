---
title: 第一课：敲打的是乐趣
date: 2021-04-06 17:37:00 +0800
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

# 前言

演讲者：李东，腾讯互动娱乐 光子工作室群 基础研究组组长。《绝地求生：刺激战场》引擎开发组长。

# 技术准备

## 编程基础

- C++（保证运行效率）&Script（保证开发效率）
- Framework（游戏开发基本框架）
  - <img src="/assets/blog_res/2021-04-06-qiaodadeshilequ.assets/Screen%20Shot%202021-04-06%20at%2017.39.20.png" alt="Screen Shot 2021-04-06 at 17.39.20" style="zoom:80%;" />
  - actor包含所有的物体，能够跟玩家发生互动的都算。组件开发：actor都是挂接不同组件进行开发的。
- Threading（多线程框架）
  - 逻辑线程+渲染线程
  - 加载的话有一到两个IO异步线程
  - 一到两个音频播放线程（音频的解码和音频的播放是单独的线程）
  - 任务线程（比较费时间的，物理模拟、压缩解压缩操作）
- Memory Pooling
- 市场上的设备占比情况
  - iOS与Android设备Top500的性能数据

## 系统知识

即与iOS或者Android设备相关的系统知识

- OOM(Out Of Memory)
- ANR(Application Not Responding)
- big.LITTLE(大小核)
- Underclocking(降频)
- Power Management
- Thermal Throttling(温度控制)

# 游戏开发

## 图形渲染

### GPU

- PowerVR(每个芯片的优化方式不一样，导致不同GPU的图形渲染管线的方式就不一样)
  - TBDR(Tile Based Deferred Rendering)
  - HSR(Hidden Surface Removal) + Early Z
- Adreno
  - IMR(Immediate Mode Rendering)
  - Adreno 3xx TBDR & Binning Pass
  - Adreno 5xx LRZ(low resolution z)
- Mali
  - TBIMR(Tile Based Immediate Mode Rendering)
  - Early Z
  - FPK(Forward Pixel Kill)

### API

- OpenGL ES(关注对于芯片的覆盖率)
- Metal：iOS唯一选择，轻量
- Vulkan：不够成熟

### 管线

- Pipeline
  - forward or deferred
  - HDR or LDR
  - Linear or Gamma
  - Culling
  - Z Pre Pass
  - Sorting
  - Post Process

### 光照

- Hack与物理方法：离线烘培、基于显卡的光线追踪技术实时预览，然后再进行美术烘培
- 多方案：手机性能差异过大
- 细节

### 模拟仿真

- 刚体碰撞
- 载具模拟
- 角色IK
- 毛发、布料、流体
- 3D重建：从照片还原3D模型
- 音效模拟：位置、室内室外，但是按照真实世界模拟计算量会很大
  - 车轮速度改变导致音效变化
  - 声音衰减（墙遮挡->射线检测）

### 多人游戏服务器

服务器架构：

![Screen Shot 2021-04-06 at 18.54.22](/assets/blog_res/2021-04-06-qiaodadeshilequ.assets/Screen%20Shot%202021-04-06%20at%2018.54.22.png)

网络延迟的处理：1. 客户端的预表现，传给服务器，服务器再回来验证，有问题的话就会拉拽；2. 推测：预测模拟第三方玩家的行为，收到服务器消息之前进行模拟

### AI

- 决策树遍历
- 图表现篮球游戏里面每个球员的势力范围，找到最好突破的点规划去篮筐的路径

# 新技术融入

- 拍照图像识别棋谱
- 微信小游戏：H5引擎

# 不断成长

- 略