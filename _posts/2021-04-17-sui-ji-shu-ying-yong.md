---
title: 第十一课：随机数在游戏中的应用
date: 2021-04-17 16:21:33 +0800
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

# 基本介绍

## 在游戏中的应用

- 游戏玩法：抽卡、开宝箱
- 模拟自然现象：火焰、植被、生物群落（火焰粒子发射器）
- 离线渲染、光线追踪
- 随机生成内容（随机关卡）

## 两种伪随机概念

**计算机概念：**

- 真随机：需要外部的随机来源如量子、噪音等等

- 伪随机：用算法生成看似随机的序列

**策划概念：**

- 真随机：每次判断都是独立的

- 伪随机：指同一类的概率事件，彼此之间存在关联性，通常保证用户体验

## 游戏中常用随机策略

- 伪随机策略：保底法（买五次必得一次铭文）

![Screen Shot 2021-04-17 at 16.32.57](/assets/blog_res/2021-04-17-sui-ji-shu-ying-yong.assets/Screen%20Shot%202021-04-17%20at%2016.32.57.png)

- 其他伪随机策略
  - 稀有道具全服控制总量
  - 洗牌算法
    - 将一个序列打乱顺序，然后挨着取这个顺序的每一个，每个都保证会被取中，比如随机听歌算法
  - 两次随机
    - 第一次抽取决定是几级铭文
    - 第二次抽取决定是具体哪种铭文

# 随机数生成器

## 随机数基本概念介绍

## 常见的伪随机数生成器

- 算法+种子
  - 游戏中常用的算法：
    - 线性同余
      - 优点：实现简单、速度快、所需内存小
      - 缺点：
        - 用作N维空间的点坐标，这些点多位于某些超平面上（看起来会有某种规律），不适合作为蒙特卡洛采样（离线渲染、光线追踪）；
        - 当m为2的幂时，低阶比特周期较短，可以通过舍弃低位来缓解
    - Xorshift
    - **梅森旋转**：周期特别长，在各种维度很均匀，缺点是需要的空间稍大（2.5KiB）
- 状态空间与周期



**关于随机数种子**

给定的种子决定了后续的随机数序列，一般程序启动时使用当前时间作为种子进行初始化

错误用法：

- 不调用srand会导致每次启动游戏获得的序列是一样的
- 每次rand之前都调用srand

**随机数种子的作用**

- 提供每次不一样的游戏体验
- 在程序生成内容（Procedural Content Generation）算法中使用，用来确保两次计算结果相同
- 在多人游戏中减少带宽占用（帧同步游戏机制）
  - 随机数种子需要同步给第三方，需要自己实现随机数生成器
- 使用非常小的录像文件来实现录像和回放功能

# 随机数分布与应用

举例：vc中的rand()只能到32767，那么如何取到0-10000的随机数？

1. 如果除以10000显然是概率非均匀分布的
2. 可以选择超过x0000的部分扔掉，拒绝采样法

问题：如何取得更大的数字，比如0-1000000？

1. 可以使用x = rand() * (RAND_MAX + 1) + rand()
2. 或者使用梅森旋转

问题：如何取得0-1的随机浮点数？

1. x = rand() / (float)RAND_MAX
2. <img src="/assets/blog_res/2021-04-17-sui-ji-shu-ying-yong.assets/Screen%20Shot%202021-04-17%20at%2021.16.28.png" alt="Screen Shot 2021-04-17 at 21.16.28" style="zoom:67%;" align='left'/>



**正态分布**

生成不同身高的人群、不同高度的树木，符合自然规律

获得正态分布：

- 拒绝采样法：
  - <img src="/assets/blog_res/2021-04-17-sui-ji-shu-ying-yong.assets/Screen%20Shot%202021-04-17%20at%2021.20.27.png" alt="Screen Shot 2021-04-17 at 21.20.27" style="zoom:50%;" align='left'/>
- Ziggurat
  - <img src="/assets/blog_res/2021-04-17-sui-ji-shu-ying-yong.assets/Screen%20Shot%202021-04-17%20at%2021.21.44.png" alt="Screen Shot 2021-04-17 at 21.21.44" style="zoom:60%;" align='left' />
- 利用正态分布CDF的反函数做Inverse transform sampling
  - <img src="/assets/blog_res/2021-04-17-sui-ji-shu-ying-yong.assets/Screen%20Shot%202021-04-17%20at%2021.24.13.png" alt="Screen Shot 2021-04-17 at 21.24.13" style="zoom:67%;" align='left'/>
- Box-Muller Transform
  - <img src="/assets/blog_res/2021-04-17-sui-ji-shu-ying-yong.assets/Screen%20Shot%202021-04-17%20at%2021.24.50.png" alt="Screen Shot 2021-04-17 at 21.24.50" style="zoom:67%;" align='left' />
- 利用中心极限定理，把m个均匀分布随机数相加
  - <img src="/assets/blog_res/2021-04-17-sui-ji-shu-ying-yong.assets/Screen%20Shot%202021-04-17%20at%2021.25.08.png" alt="Screen Shot 2021-04-17 at 21.25.08" style="zoom:67%;" align='left'/>

## 小游戏

## 几何形状采样与基本分布采样

在某个X形区域内产生多少个怪物的问题：

<img src="/assets/blog_res/2021-04-17-sui-ji-shu-ying-yong.assets/Screen%20Shot%202021-04-17%20at%2021.28.44.png" alt="Screen Shot 2021-04-17 at 21.28.44" style="zoom:60%;" align='left'/>

## 洗牌算法

![Screen Shot 2021-04-17 at 21.30.28](/assets/blog_res/2021-04-17-sui-ji-shu-ying-yong.assets/Screen%20Shot%202021-04-17%20at%2021.30.28.png)