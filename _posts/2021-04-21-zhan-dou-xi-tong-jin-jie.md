---
title: 第十七课：核心逻辑设计——战斗系统进阶
date: 2021-04-21 16:37:00 +0800
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

# 第一章：网络问题

## 实际网络环境会导致的情况

**实际的网络环境：**

![Screen Shot 2021-04-21 at 16.39.49](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.39.49.png)

**导致的问题：**

- 出手的粘滞感
- combo技能由于网络波动无法继续
  - 由于网络波动，上行到服务器的消息比预期的要迟，导致combo技能超时被打断
- 特殊引导技能由于网络波动，导致技能之间动作不连贯
  - 网络波动导致下行包到达客户端的时间不符合预期

## Req-Cache/Rsp-Cache

<img src="/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.41.52.png" alt="Screen Shot 2021-04-21 at 16.41.52" style="zoom:70%;" />

# 第二章：性能问题

性能问题的瓶颈在于CPU、流量和内存，从1V1到1000人混战的转变

## CPU性能问题

![Screen Shot 2021-04-21 at 16.44.14](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.44.14.png)

- 强交互高实时性要求
- 毛刺和雪崩
  - 玩家的随机聚集导致毛刺进而导致雪崩
  - 削峰平谷

## 流量性能问题

![Screen Shot 2021-04-21 at 16.46.23](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.46.23.png)

## 内存性能问题

![Screen Shot 2021-04-21 at 16.47.12](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.47.12.png)

## 性能问题汇总

![Screen Shot 2021-04-21 at 16.47.44](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.47.44.png)

# 第三章：可维护性问题

## 容灾

![Screen Shot 2021-04-21 at 16.48.10](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.48.10.png)

![Screen Shot 2021-04-21 at 16.48.27](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.48.27.png)

## 开发效率问题

![Screen Shot 2021-04-21 at 16.48.55](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.48.55.png)

## 团队配合问题

![Screen Shot 2021-04-21 at 16.49.30](/assets/blog_res/2021-04-21-zhan-dou-xi-tong-jin-jie.assets/Screen%20Shot%202021-04-21%20at%2016.49.30.png)

**例子：buff成环的问题：**

buff是通过配置文件交给策划的，但是策划配置的buff效果可能导致buff循环叠加，这只能由开发者在早期解决这个问题，而不是把锅抛给策划。

