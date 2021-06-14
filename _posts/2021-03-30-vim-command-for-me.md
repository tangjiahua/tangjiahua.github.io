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

# Vim常用命令

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

## 文件中移动

```shell
通过:10可以直接移动光标到文件第10行。如果你看不到行号，可以:set number。 gg移到文件首行，G移到尾行。

拷贝整个文件：ggyG。

/xx可以查找某个单词xx，n查找下一个，N查找上一个。 在光标跳转之后，可以通过c-o返回上一个光标位置，c-i跳到下一个光标位置。

?xx可以反向查找，q/, q?可以列出查找历史。
```

# Terminal常用命令

## 移动操作

```shell
在Mac系统中并没有Home、End等键，所以在使用时并不是特别的顺手，但是有几个键位组合可以使Terminal的操作更加灵活方便。

将光标移动到行首：control + a
将光标移动到行尾：control + e
清除屏幕：control + l
搜索以前使用命令：control + r
清除当前行：control + u
清除至当前行尾：control + k
单词为单位移动：option + 方向键
```

