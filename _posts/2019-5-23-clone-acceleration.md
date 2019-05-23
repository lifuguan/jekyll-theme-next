---
title:  解决`git clone`速度太慢的方法
date: 2019-5-23 19:00:00
categories:
- GIT
- TX2
tags:
---


## 提示：必须拥有SSR或SS并保持开启

1. 使用命令 `git config --global http.proxy 'socks5://127.0.0.1:1080' `
2. 完成，可以发现速度变快