---
title: 第十八课：MMORPG AI系统设计与实现
date: 2021-04-21 17:07:00 +0800
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

# 第一章：MMORPG AI基础

## MMORPG AI简历

什么是MMORPG AI

游戏内NPC能够通过环境或事件的变化进行逻辑判断，从而同玩家进行产生特定的行为交互。它主要包括三个部分：感知 -> 决策 -> 行动。

- 感知：侦测周围环境变化的能力，如玩家进入视野、受到攻击
- 决策：根据环境变化思考做出何种反馈，是整个AI框架主要的构成部分，常见的有状态机、行为树
- 行动：NPC做出的具体反馈，如释放技能、寻路等操作

MMORPG AI架构

AI在顶层，下层包括寻路、移动、技能、 视野

## 朴素的AI-Hard Code

直接用if-else语句就可以编写AI，然而遇到更复杂的AI的话if-else会写很多，对所有对象都要写if-else，并且针对不同的对象想要复用是很困难的。

![Screen Shot 2021-04-22 at 10.39.29](/assets/blog_res/2021-04-21-AI-xi-tong-she-ji-yu-shi-xian.assets/Screen%20Shot%202021-04-22%20at%2010.39.29.png)

## 有限状态机

**状态机3要素**

- 现态：当前所处的状态
- 事件：当一个事件发生，将会触发一个动作，或者执行一次状态的迁移
- 动作：条件满足后执行的动作

![Screen Shot 2021-04-22 at 10.42.30](/assets/blog_res/2021-04-21-AI-xi-tong-she-ji-yu-shi-xian.assets/Screen%20Shot%202021-04-22%20at%2010.42.30.png)

因此前面野猪AI的例子实现如下：

![Screen Shot 2021-04-22 at 10.43.00](/assets/blog_res/2021-04-21-AI-xi-tong-she-ji-yu-shi-xian.assets/Screen%20Shot%202021-04-22%20at%2010.43.00.png)

一般为每种状态定义一个基类，不同的NPC派生自基类，只要实现它与众不同的接口即可，使得AI复用成为可能。

然而真实游戏里面的状态流转图相当复杂，并且扩展困难，难以维护，新加状态需要考虑与已有状态间的关系，策划不能充分参与其中，只能有程序来完成。

## 行为树 —— Behavior Tree

- 节点分为控制节点、条件节点、行为节点
- 条件节点、行为节点执行都有一个结果（成功、失败、运行中）
- 控制节点根据返回结果执行下一步动作

![Screen Shot 2021-04-22 at 10.46.29](/assets/blog_res/2021-04-21-AI-xi-tong-she-ji-yu-shi-xian.assets/Screen%20Shot%202021-04-22%20at%2010.46.29.png)

![Screen Shot 2021-04-22 at 10.46.48](/assets/blog_res/2021-04-21-AI-xi-tong-she-ji-yu-shi-xian.assets/Screen%20Shot%202021-04-22%20at%2010.46.48.png)

ps：Se就是顺序执行子节点，如果有返回false的就直接回溯，不会继续顺序执行子节点，直到所有子节点都返回了true；而P是不管子节点返回什么都会去执行一次。

![Screen Shot 2021-04-22 at 10.48.51](/assets/blog_res/2021-04-21-AI-xi-tong-she-ji-yu-shi-xian.assets/Screen%20Shot%202021-04-22%20at%2010.48.51.png)

这个好处就是你会有一个编辑器，甚至可以交给策划来做，编辑器会帮你生成这个行为树

![Screen Shot 2021-04-22 at 10.49.38](/assets/blog_res/2021-04-21-AI-xi-tong-she-ji-yu-shi-xian.assets/Screen%20Shot%202021-04-22%20at%2010.49.38.png)

## 总结

结合上面三种AI形式，可以将他们结合起来，行为树虽好，但是执行的开销非常大，所以以野猪AI为例，我们对于逃跑、巡逻、死亡的状态（比较通用，因为其他的对象AI也可能会用到这种状态）就使用状态机，而对于攻击状态里面的技能决策，我们又让其选用行为树。

# 第二章：MMORPG AI寻路

## 直线寻路

直线生成路径，然而有阻挡的时候就用不了。

## 贪心寻路

- 每次都朝着缩短xy方向中距离较近者的方向逼近一步
- 如果某个方向不能走，就尝试另一个方向

## A*寻路

略

## 导航网格寻路

先找出网格，再找出路径，速度会加快很多（？）

![Screen Shot 2021-04-22 at 10.58.16](/assets/blog_res/2021-04-21-AI-xi-tong-she-ji-yu-shi-xian.assets/Screen%20Shot%202021-04-22%20at%2010.58.16.png)