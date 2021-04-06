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

# 新技术融入

# 不断成长