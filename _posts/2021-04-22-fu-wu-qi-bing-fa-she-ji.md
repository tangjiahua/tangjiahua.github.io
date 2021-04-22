---
title: 第二十二课：服务器并发设计
date: 2021-04-22 13:28:00 +0800
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

# 第一章：并发的概念

## 并发vs并行

并行(Parallel)：程序的一个状态，有多个程序同时进行，多线程或者多进程是实现的手段。一个执行流可以模拟出一个并发的效果。

并发(Concurrent)：程序的多个操作，可以在同样的时间段内重叠进行。

并发是并行的一个子集，并行可以用来实现并发。

```c++
你吃饭吃到一半，电话来了，你一直到吃完了以后才去接，这就说明你不支持并发也不支持并行。
你吃饭吃到一半，电话来了，你停了下来接了电话，接完后继续吃饭，这说明你支持并发。
你吃饭吃到一半，电话来了，你一边打电话一边吃饭，这说明你支持并行。

并发的关键是你有处理多个任务的能力，不一定要同时。
并行的关键是你有同时处理多个任务的能力。

所以我认为它们最关键的点就是：是否是『同时』。



作者：「已注销」
链接：https://www.zhihu.com/question/33515481/answer/58849148
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

<img src="/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.02.28.png" alt="Screen Shot 2021-04-22 at 14.02.28" style="zoom:67%;" />

# 第二章：并发技术选型

## 并发选型

### 结构并发

<img src="/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.03.40.png" alt="Screen Shot 2021-04-22 at 14.03.40" style="zoom:50%;" />

### 状态并发

<img src="/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.03.49.png" alt="Screen Shot 2021-04-22 at 14.03.49" style="zoom:50%;" />

### 混合并发：无阻塞+高并发

<img src="/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.04.18.png" alt="Screen Shot 2021-04-22 at 14.04.18" style="zoom:50%;" />

## 时间分片设计

![Screen Shot 2021-04-22 at 14.05.39](/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.05.39.png)

### 异步回调流程

![Screen Shot 2021-04-22 at 14.07.11](/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.07.11.png)

![Screen Shot 2021-04-22 at 14.07.43](/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.07.43.png)

## 高端方式：协程（用户态线程）

![Screen Shot 2021-04-22 at 14.08.25](/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.08.25.png)

## 游戏服务器的多线程和多进程考虑

![Screen Shot 2021-04-22 at 14.09.27](/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.09.27.png)

**线程的使用场景：**

- 协议打包解包
- 接入服务
- 存储服务
- 对于简单的游戏，一个玩家一个线程是可以的；对于MMORPG一个玩家一个线程，都在同一个进程的话，会出问题，玩家和玩家的交互比较频繁，因此线程的切换非常快速，需要加上各种锁才行，但是这显然是很麻烦的做法。

# 第三章：集群和负载均衡

## 负载均衡常用策略

- 业务：地图场景
  - 轮询
  - 随机
  - 最小响应时间
  - 最小并发数
  - 最小承载
  - 哈希：如接入/存储
  - 分布式哈希等等

**以天刀为例子：**

![Screen Shot 2021-04-22 at 14.13.42](/assets/blog_res/2021-04-22-fu-wu-qi-bing-fa-she-ji.assets/Screen%20Shot%202021-04-22%20at%2014.13.42.png)

