---
title: 第八课：游戏逻辑与反外挂
date: 2021-04-10 14:17:00 +0800
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

# 游戏逻辑服务器

## 游戏逻辑服务器

**游戏服务器整体架构：**

![Screen Shot 2021-04-10 at 14.19.46](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2014.19.46.png)

**游戏服务器的作用**

- 游戏数据存储
- 与其他玩家交互的中转
- 玩法驱动和逻辑
- 反外挂和防作弊（韩国上网实名制，所以反外挂逻辑的一般都在客户端，而不会在服务器判断）

**游戏服务器状态图**

![Screen Shot 2021-04-10 at 14.24.42](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2014.24.42.png)

时间间隔驱动：时间中断出去检查是否有一些相关逻辑需要处理，比如发现某个计时器倒计时结束

## 以3D MMORPG为例子阐述服务器程序的实现

### 游戏对象管理

![Screen Shot 2021-04-10 at 14.28.40](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2014.28.40.png)

### 地图的描述

![Screen Shot 2021-04-10 at 14.37.25](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2014.37.25.png)

将其转换成0与1的二维数组，以达到判断能不能走到某些位置的目的。

### 地图上玩家的管理

以32*32的大小，把地图分成N个区域，每个区域里面的玩家、NPC等玩家，弄成链表

![Screen Shot 2021-04-10 at 14.38.36](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2014.38.36.png)

**为什么需要视野管理？**

![Screen Shot 2021-04-10 at 14.39.26](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2014.39.26.png)

### 视野管理

确定服务器能承受的最大的视野对象数量N（如何确定？）

- 与同类产品比较
- 用机器人去跑压力测试看最大承载量

假设需要进行筛选的话，可以用如下的方法筛选显示：

![Screen Shot 2021-04-10 at 14.43.40](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2014.43.40.png)

视野对称性就是你看得到他，他也要看得到你。

### 玩家移动

![Screen Shot 2021-04-10 at 14.46.17](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2014.46.17.png)

### 玩家攻击

![Screen Shot 2021-04-10 at 16.06.38](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2016.06.38.png)

### 物品掉落和拾取

![Screen Shot 2021-04-10 at 16.12.03](/assets/blog_res/2021-04-10-you-xi-luo-ji-yu-fan-wai-gua.assets/Screen%20Shot%202021-04-10%20at%2016.12.03.png)



# 外挂与反外挂

**外挂导致的后果：**

- 没有检查玩家与传送NPC距离，导致玩家随时随地传送
- 视野不可见、攻击距离、伤害数值、使用还没有学习的技能
- 绕过客户端，使用廉价材料打造出高级宝石来卖钱

- 破解协议，被打金工作室盯上

**外挂可以作弊成功的根本原因：**

- 服务器逻辑有bug
- 异常情况考虑不全面
- 无法保证消息来源的可靠性

**逻辑服务器如何应对：**

- 谨慎的编码风格
- 完善的监控告警
- 提高外挂的作弊成本
- 限制外挂的获利收入
- 分析工作室的行为模式，批量打击

## 反外挂的建议

1. 不信任客户端请求
   1. 上行包所有数据都要检查合法性
   2. 越界、指针、溢出、类型匹配等检查
   3. 不信任度累计机制
2. 提高外挂作弊成本
   1. 服务器负责计算然后下发（结算、奖励），隐藏中间数据
   2. 图片答题机制（验证码等）
   3. 动态代码（关键操作经常变化，调用下发的动态链接库的代码）
   4. 对于外挂的试探性请求包，进行记录和惩罚
3. 限制外挂的获利收入
   1. 先扣，再操作
   2. 操作失败，防止多退
   3. 上限限制、上限告警（经验、金钱）
   4. 大部分活动获得的收益是绑定的，只有少部分活动能够得到可交易的收益，每次变动都迫使外挂做出重大修改
4. 打击打金工作室
   1. IP/MAC限制
   2. 操作频率控制
   3. 基于“数据挖掘”，通过离线策略的学习和验证策略、发觉异常数据、发掘打币或作弊工作室