---
title: 第二课：游戏服务器架构概要
date: 2021-04-06 20:03:00 +0800
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

# 《轩辕传奇》——MMORPG分区多世界的服务器架构

## 运营的视角

![Screen Shot 2021-04-06 at 20.09.49](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2020.09.49.png)

## 运维的视角

![Screen Shot 2021-04-06 at 20.11.46](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2020.11.46.png)

## 客户端的视角

![Screen Shot 2021-04-06 at 20.13.48](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2020.13.48.png)

大世界（无缝地图）：将一个大地图分成不同的区域，每个区域用一个进程去承载，所有控制也需要一个主进程去承载。

跨世界共享：不同世界接触到的相同东西，单独提出来作为公共服务进行处理。主备从架构。

逻辑处理和持久化数据再同一个物理机上遇到的问题：

- DB的IO太多
- 日志文件
- 物理机故障

将相对独立、变化少的功能（如邮件系统）拆分出来。

慎用多线程，除非只有单一职责，否则不要用多线程。主线程里逻辑太过复杂会需要添加很多锁。

切分的原则：

![Screen Shot 2021-04-06 at 20.35.45](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2020.35.45.png)

## 接入与负载

![Screen Shot 2021-04-06 at 20.39.58](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2020.39.58.png)

## 可用性

![Screen Shot 2021-04-06 at 20.43.53](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2020.43.53.png)

## 在线控制

![Screen Shot 2021-04-06 at 20.47.00](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2020.47.00.png)

GM系统：管理员系统，通过聊天室上传，给GM开通权限。

经分系统：对日志进行解析，连接到一个展示页面。

## 过载保护

![Screen Shot 2021-04-06 at 20.53.27](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2020.53.27.png)

hacker用户非正常高频请求。

## DB设计

![Screen Shot 2021-04-06 at 21.03.38](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2021.03.38.png)

# 《轩辕传奇》——各类服务介绍

## 版本升级

![Screen Shot 2021-04-06 at 21.04.51](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2021.04.51.png)

版本服务器进行版本管理。

## 目录服务

![Screen Shot 2021-04-06 at 21.05.45](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2021.05.45.png)

每段时间上报一下。

## 角色登录

world/scene

![Screen Shot 2021-04-06 at 21.06.36](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2021.06.36.png)

难点：跨进程的异步事务的复杂，到引入协程。

## 运营支持

![Screen Shot 2021-04-06 at 21.12.20](/assets/blog_res/2021-04-06-kehuduanjishuzongshu.assets/Screen%20Shot%202021-04-06%20at%2021.12.20.png)

脏字过滤：起名系统、聊天系统；同一套组建加不同的策略。

验证码过滤：恶意挂机问题。AI进行识别真人玩家与挂机脚本。

