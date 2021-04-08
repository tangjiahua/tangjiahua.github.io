---
title: 第五课：分布式系统设计
date: 2021-04-07 16:20:00 +0800
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

# 分布式系统概览

分布式系统指分布在硬件设备上的多个软件组件，彼此通过网络来通信和协作的系统。

分布式系统需要考虑的问题包括：业务模块划分、负载均衡、融在容错、网络通信等

消息队列：专门负责消息传递的通用中间件。特点：解耦发送方和接收方、稳定可靠

感性认识分布式系统：

![Screen Shot 2021-04-08 at 20.52.21](/assets/blog_res/2021-04-07-fen-bu-shi-xi-tong.assets/Screen%20Shot%202021-04-08%20at%2020.52.21.png)

# 分布式系统中间件

## 腾讯游戏通信方案-TBUS（进程间通信）

- TBUS地址
  - World.Zone.Func.Instance
  - 微信.一区.pvp战斗进程.1号
- 例子
  - 进程A：1.1.2.1；进程B：1.1.3.1；
  - TBUSD A：1.1.1.1；TBUSD B：1.1.1.2；

<img src="/assets/blog_res/2021-04-07-fen-bu-shi-xi-tong.assets/Screen%20Shot%202021-04-08%20at%2020.31.53.png" alt="Screen Shot 2021-04-08 at 20.31.53" style="zoom:100%;"/>

通过GCIM（全局的路由配置信息）/GRM两套配置管理工具，tbusd(A)就可以知道tbusd(B)在哪台机器上。

![Screen Shot 2021-04-08 at 20.39.26](/assets/blog_res/2021-04-07-fen-bu-shi-xi-tong.assets/Screen%20Shot%202021-04-08%20at%2020.39.26.png)

TBUS Channel是共享内存做的。是进程和tbusd之间进行交流方式。

![Screen Shot 2021-04-08 at 20.44.14](/assets/blog_res/2021-04-07-fen-bu-shi-xi-tong.assets/Screen%20Shot%202021-04-08%20at%2020.44.14.png)

TBUS特点：

- 屏蔽部署细节
  - 通过TBUS ID替代IP地址和Port
  - TBUS ID作为抽象，覆盖了下层细节
  - IP地址变更也不会修改TBUS ID
- 程序重启影响小
  - 网络层被托管
    - 无需建立连接
    - 不会丢失网络上的消息
  - 快速回复
    - 重启后从TBUS共享内存中继续接收消息。
- 性能强大
  - 无锁化实现
  - 纯内存操作

## 通信格式

- 关键点
  - 序列化（发送前按照一定规则进行编码格式，写成二进制流发出去）/反序列化（按照相同的规则把数据还原回原有的消息格式）
  - 版本兼容：接收方要能同时处理不同版本的消息
  - 打包解包性能一定要高
- 解决方法
  - Protocol Buffers - Google
  - TDR - Tencent

### Protocol Buffer

![Screen Shot 2021-04-08 at 20.55.46](/assets/blog_res/2021-04-07-fen-bu-shi-xi-tong.assets/Screen%20Shot%202021-04-08%20at%2020.55.46.png)

proto文件是一个xml文件，内部定义一个结构、结构体是如何表示的，通过proto文件表述，proto文件通过代码生成器转换成代码（如C++），编译后会集成到发送方的消息里面，序列化后会通过网络发送出去。接收方解码器解码后还原成原始消息。

## 并发模型

