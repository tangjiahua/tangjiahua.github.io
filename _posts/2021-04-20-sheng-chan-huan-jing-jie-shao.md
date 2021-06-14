---
title: 第十四课：生产环境介绍
date: 2021-04-20 22:15:00 +0800
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

# 介绍生产环境和开发环境的差异

## 生产环节的定义、要素

线上环境、生产环节都一个意思，略过。

## 开发环境的主要差异

|      | 开发环境                           | 生产环境                                 |
| ---- | ---------------------------------- | ---------------------------------------- |
| 规模 | 几十台机器构成，供少量开发人员使用 | 上千台机器，为海量用户提供服务           |
| 网络 | 局域网，网速稳定，无波动           | 广域网，用户网速波动频繁，有被攻击的风险 |
| 稳定 | 按需启停，基本无强制性要求         | 应对各种突发事故，确保高可用性           |
| 更新 | 不受限制，快速迭代                 | 根据版本节奏，严格控制，按计划更新       |

# 机型选择

- 易用性
- 服务质量
- 业务特点
- 成本

## 接入层、逻辑层、存储层的划分

![Screen Shot 2021-04-20 at 22.22.29](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.22.29.png)

## 不同层级对机型的要求

<img src="/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.23.06.png" alt="Screen Shot 2021-04-20 at 22.23.06" style="zoom:50%;" />

<img src="/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.23.43.png" alt="Screen Shot 2021-04-20 at 22.23.43" style="zoom:50%;" />

# 网络架构

## 网络层次模型介绍

学校学过，不介绍了

**腾讯网络架构：**

![Screen Shot 2021-04-20 at 22.24.58](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.24.58.png)

## 统一接入、防攻击、安全隔离、流量调度的实现

### 统一接入

![Screen Shot 2021-04-20 at 22.25.34](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.25.34.png)

### 防攻击

![Screen Shot 2021-04-20 at 22.26.07](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.26.07.png)

### 安全隔离

![Screen Shot 2021-04-20 at 22.26.28](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.26.28.png)

### 流量调度

![Screen Shot 2021-04-20 at 22.26.56](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.26.56.png)

# 机房要求

## 机房架构介绍

![Screen Shot 2021-04-20 at 22.27.43](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.27.43.png)

## 基础设置可靠性

### 配电可靠性

![Screen Shot 2021-04-20 at 22.28.24](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.28.24.png)

**这样做的话可靠性可以大于等于99.995%**

### 制冷可靠性

![Screen Shot 2021-04-20 at 22.29.19](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.29.19.png)

### 通信可靠性

![Screen Shot 2021-04-20 at 22.30.07](/assets/blog_res/2021-04-20-sheng-chan-huan-jing-jie-shao.assets/Screen%20Shot%202021-04-20%20at%2022.30.07.png)

## 机房布局介绍

腾讯的机房布局就略过了。

# 总结

- 合适的机型
  - 计算所需资源，挑选性价比最高的方案
  - 冗余备机种类和数量
- 网络接入方案
  - 明确网络延迟要求，计算网络流量大小
  - 是否需要多线接入，跨网的延迟容忍度
- 机房分布
  - 架构特性
  - 用户的地理分布