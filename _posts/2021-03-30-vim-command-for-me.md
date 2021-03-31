---
title: 我的vim常用命令
date: 2021-03-30 15:52:33 +0800
categories: [基础技术]
tags: [技术]
pin: true
author: Tang Jiahua

toc: true
comments: true
Typora-root-url: ..
math: false
mermaid: true
---

# 我的常用命令

## 删除操作

```shell
dw:删除从光标开始后面的字符
daw:删除光标所在的词
bdw:跳回光标所在该单词开头，然后删除
dd:删除一行

```

## 移动操作

```shell
# 字符移动
w:移动到下一个单词首
b:移动到上一个单词首
e:移动到下一个单词结尾
ge:移动到上一个单词结尾
^:移动到行首
$:移动到行尾

# 相对屏幕移动
ctrl+f
ctrl+b
ctrl+e:按行下滚
ctrl+y:按行上滚
H:移动到屏幕首行
L:到屏幕尾行
M:到屏幕中间
zt:置顶当前行
zz:将当前行移动到屏幕中部
zb:将当前行移动到底部

```

