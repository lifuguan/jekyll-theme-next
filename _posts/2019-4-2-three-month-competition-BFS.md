
---
title:  学校选拔赛（DFS&BFS&迷宫问题）-总结
date: 2019-4-1 13:00:00
categories:
- Algorithm
- C++
tags:
- BFS
- DFS
- 迷宫问题
---

<script type="text/javascript"
       src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

## Problem Description
给定一个迷宫，入口为左上角，出口为右下角，问是否有路径从入口到出口，若有则输出一条这样的路径。注意移动可以从上、下、左、右、上左、上右、下左、下右八个方向进行。迷宫输入0表示可走，输入1表示墙。易得`可以用1将迷宫围起来避免边界问题`。


