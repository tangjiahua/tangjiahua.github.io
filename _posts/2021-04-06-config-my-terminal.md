---
title: 配置我的终端
date: 2021-04-06 01:08:00 +0800
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

# 序言

本文主要目的是帮助自己快速配置本地终端。

# 功能介绍

我的私人oh-my-zsh配置包括如下：

**插件配置**：auto-suggestions, auto-syntax-highlighting, git

**代理配置**：调用proxy_on或proxy_off可以开启终端的代理，这要配合clashX使用

**vim配置**：vim配置文件在/jiahua目录下，叫做.vimrc

**alias配置**：快速调用应用

# 流程

## 插件配置

通过$ cat /etc/shells查看shells

如果系统中没有zsh，则需要安装：

```shell
// Linux
$ sudo yum install zsh    (Fedora和RedHat以及SUSE中)或
$ sudp apt-get install zsh    (Debian系列，Ubuntu )

// macOS 系统自带了zsh, 一般不是最新版，如果需要最新版可通过Homebrew来安装(确认安装了Homebrew)
$ brew install zsh zsh-completions

// 或者也可以使用MacPorts(包管理工具)
$ sudo port install zsh zsh-completions
```

设置当前默认shell\

```shell
$ echo $SHELL    //把zsh设为默认shell，如果shell列表中没有zsh或者你没有使用chsh权限的时候，不起作用
       
$ [sudo] chsh -s $(which zsh) 或，
$ chsh -s /bin/zsh
```

安装oh-my-zsh

```shell
# clone下来我的私人oh-my-zsh配置
git clone --recursive https://github.com/tangjiahua/ohmyzsh.git ~/.oh-my-zsh

# 安装配置文件
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

# 使配置生效
source ~/.zshrc
```

## 代理配置

安装clashX并配置好代理

```shell
# 执行如下shell命令
proxy_on
```

## vim配置

安装vim（macOS一般是自带vim的，如果没有的话使用brew安装）

```shell
# 复制配置文件
cp ~/.oh-my-zsh/jiahua/.vimrc ~/.vimrc

# 启动配置
source ~/.vimrc
```

## alias配置

```shell
# 本配置文件的alias配置如下

# 需要安装typora应用程序
alias typora="open -a typora"
alias ls="ls -al"
```

