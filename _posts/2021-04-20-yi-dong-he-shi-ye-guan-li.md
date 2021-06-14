---
title: 第十五课：移动和视野管理
date: 2021-04-20 23:10:00 +0800
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

# 为什么需要数据同步

简单来说，网络游戏需要数据同步玩家的状态与动作。

# 最常见的同步“移动同步”

## 2D移动的实现

### **玩家移动的表达一（移动向量）：**

- POS当前的位置
- DIR朝向
- V速度

**同步的时机：**

- 转向
- 变速
- 停止

![Screen Shot 2021-04-20 at 23.14.03](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-20%20at%2023.14.03.png)

解释：

**上行延迟**直接拖拽的情况：上行数据包延迟过大，到达服务器太晚了，服务器如果发现这个位移包在原来走过的路径上，那就将该角色直接恢复拖拽到原来的那个位置，在游戏里面延迟大的时候就是表现为“走不动”。

**上行延迟**加一个固定时长：每次只能走0.5秒，如果超过0.5秒没有发包过来，也就是出现延迟的话，那就让该角色停下来不要动，即需要定时上传移动包。

**下行延迟**运动补偿的情况：快速将对方用户拉到应该去的位置，就是比较快速的方法运动过去，游戏里面的表现就是“突然他跑得很快跑过去了”

**丢包会怎么样？**

比如在传送移动包的时候丢包了，然后后面的包继续上传，服务器接收到最新的包发现和现在的位置差别太大就会拒绝这个包，将用户拖拽回原来的位置。

### 玩家移动的表达二（路点表示法）：

![Screen Shot 2021-04-20 at 23.22.55](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-20%20at%2023.22.55.png)

**路点表示法延迟的处理：**

![Screen Shot 2021-04-20 at 23.46.42](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-20%20at%2023.46.42.png)

## 3D地形概念

![Screen Shot 2021-04-20 at 23.52.30](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-20%20at%2023.52.30.png)

补充：大部分时候确定移动对象在空间的位置也用不到z，只要有layer就可以了。因为天刀中有轻功，所以在确定位置的时候也用到了z这个量。

**以天刀为例子介绍：**

![Screen Shot 2021-04-20 at 23.56.40](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-20%20at%2023.56.40.png)

## 3D地形上的移动

![Screen Shot 2021-04-20 at 23.58.16](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-20%20at%2023.58.16.png)

# 移动中视野的管理

## 为什么需要视野管理

![Screen Shot 2021-04-21 at 10.49.14](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-21%20at%2010.49.14.png)

剪枝：也就是发送技能之后只选择会受到技能影响的附近的几个玩家来进行影响。

## 视野管理的经典实现-九宫格

这个九宫格和grid格子不一样，grid的粒度太小了，没有意义。

![Screen Shot 2021-04-21 at 10.50.46](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-21%20at%2010.50.46.png)

## 九宫格种角色移动的处理

![Screen Shot 2021-04-21 at 10.51.11](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-21%20at%2010.51.11.png)

发送消息给第三方，比如actor_leave()这样的包过去，表示有人离开“我”的视野。

## Around的经典实现-十字链表

![Screen Shot 2021-04-21 at 10.52.24](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-21%20at%2010.52.24.png)

需要两个排序，一是按X排序所有玩家的一条链表，二是按Y排序所有玩家的一条链表。

## 十字链表角色移动的处理

![Screen Shot 2021-04-21 at 10.53.49](/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-21%20at%2010.53.49.png)

old_set和new_set的计算简单在于，链表可以直接向前和向后回溯很快能找到在集合内的玩家。找出两个链表中的玩家，然后取交集就是一个我们需要的set。

## 两种方式的比较

<img src="/assets/blog_res/2021-04-20-yi-dong-he-shi-ye-guan-li.assets/Screen%20Shot%202021-04-21%20at%2010.55.45.png" alt="Screen Shot 2021-04-21 at 10.55.45" style="zoom: 67%;" />

