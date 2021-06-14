---
title: 第四课：游戏后台开发工具
date: 2021-04-07 14:56:00 +0800
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

# 开发语言

C++新特性：auto, nullptr, decltype, lamda, constexpr

找mentor拿到项目组的代码规范、开发流程规范。

# 开发环境

Linux系统监控系统命令：perf, vmstat, gdb, trace, top, ifconfig, ulimit, lsof

# 腾讯开发组件介绍

## tsf4g(Tencent Service Framework For Game)

### 1 接入层 - TGW

- TGW(Tencent Gateway)
- 支持自动负载均衡的系统
- 可靠性高、扩展性强、性能高、抗攻击能力强

![Screen Shot 2021-04-07 at 15.34.25](/assets/blog_res/2021-04-07-kai-fa-gong-ju.assets/Screen%20Shot%202021-04-07%20at%2015.34.25.png)

### 2 接入层 tconnd

- 腾讯网络接入公共组件
- 为不同应用场景（TCP、UDP、HTTP）提供网络接入服务
- 权限校验（验证、核对身份）

![Screen Shot 2021-04-07 at 15.36.39](/assets/blog_res/2021-04-07-kai-fa-gong-ju.assets/Screen%20Shot%202021-04-07%20at%2015.36.39.png)

### 3 消息队列 tbus

- tbus基于共享内存构建无锁双通循环消息队列，发送的双方通过专用的读写队列完成数据收发，实现本地进程通信或者远程进程通信。
- 通信双方使用两个队列称为tbus通道，每一组通信双方需要一个tbus通道。

![Screen Shot 2021-04-07 at 15.38.48](/assets/blog_res/2021-04-07-kai-fa-gong-ju.assets/Screen%20Shot%202021-04-07%20at%2015.38.48.png)

### 4 逻辑层 swift

- swift是TBase组件中TApp应用程序框架的扩展组件，它在TApp应用程序框架的基础上提供了同步和异步事务处理能力，封装了TBus、Socket等多种网络通信方式，提供定时器等基础系统，极大的简化了应用逻辑程序的开发难度。

![Screen Shot 2021-04-07 at 15.41.40](/assets/blog_res/2021-04-07-kai-fa-gong-ju.assets/Screen%20Shot%202021-04-07%20at%2015.41.40.png)

### 5 数据层 tcaplus(TTC, CKV)

- TCaplus全托管的分布式存储平台产品
- 针对游戏的开发特点和运维需求进行定制，具有高性能、低成本等特点，实现了不停服无损扩容和全Web化的系统管理，替代传统的存储服务。

### 6 TCM进程集中管理系统

- Tencent Center Manager是TSF4G解决方案的基础系统之一，作用时在运营过程中对游戏进程进行统一控制管理。
- 业务进程部署信息集中管理
- 业务进程启动停止、状态检查、自动拉起控制
- 业务进程配置文件自动生成和传送
- 业务进程tbus通信关系的自动生成和更新

### 7 其他主要组成

- TDir 目录服务
- TVersion 版本服务器
- TRank 业务排行服务
- TLock 锁服务

## QQ农场的架构

![Screen Shot 2021-04-07 at 15.57.27](/assets/blog_res/2021-04-07-kai-fa-gong-ju.assets/Screen%20Shot%202021-04-07%20at%2015.57.27.png)

# 网络通信

Protobuf

tdr

进程同步：指多个进程在特定点会合或者握手使得达成协议或者使得操作序列有序。数据同步指一个数据集的多份拷贝一致以维护完整性。常用进程同步原语来实现数据同步。

异步：非阻塞、协程、并发

# 业务框架介绍

日志：日志会造成性能问题。考虑日志的级别定义。

测试：写完一个模块，补充GTest测试用例。保证未来重构之后，前面这些测试用例是能够通过的。

防灾演习：当某一个节点挂掉的时候，整个服务的情况会是怎样的，应当怎么进行补充或者是急救措施。

发布：

- DO分离：专人专享，开发不解决外网的问题，即运营的问题
- 职能化：将通用解决方案沉淀下来
- 灰度发布：逐步发布服务
- 发布服务器的步骤、服务器重启停止

