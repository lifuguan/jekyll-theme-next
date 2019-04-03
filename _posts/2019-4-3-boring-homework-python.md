---
title:  第六次python上机作业
date: 2019-4-3 16:30:00
categories:
- homework
- Python
---

## **Question one**
### Explanation
一行代码遍历从1-1999得素数
### Code
```python
from math import sqrt
def proc(query):
    list = [ p for p in   range(1, 2000) if 0 not in [ p% d for d in range(2, int(sqrt(p))+1)] ]
    for a in list:
        if a == 1999:
            print("no")
        elif a == query:
            print("yes")
            break

query = eval(input())
proc(query)
```


## **Question two**
### Explanation
递归算法-辗转相除法
### Code
```python
origin_a = 0
origin_b = 0
def lowestCommonDivisor(a , b):
    
    b , a = a, b % a  
    if a == 0:
        print(origin_a * origin_b / b)
        return b
    else:
        return lowestCommonDivisor(a , b)

origin_a = eval(input())
origin_b = eval(input())
res = lowestCommonDivisor(origin_a, origin_b)
print(res)
```

## **Question three**
### Explanation
看题目写代码裸题
### Code
```python
import math
def boring(a):
    Xn = a
    XnPlus = 0.5 * (Xn + (a / Xn))
    while math.fabs(XnPlus - Xn) < 1e-3:
        XnPlus = 0.5 * (Xn + (a / Xn))
        Xn = XnPlus
    print(XnPlus)

boring(eval(input("input:")))
```


## **Question four**
### Explanation
将之前得作业复制到函数里面就好
### Code
```python
def funcname(origin_list):
    tot = 0
    max_ = 0
    min_ = 0
    for p in range(len(origin_list)) :
        max_ = max(max_, p)
        min_ = min(min_, p)
        tot += p
    ser = eval(input())
    counter = 0
    for a in origin_list:
        if a == ser:
            counter += 1
    print(tot, "  ",max_,  "  ", min_,  "   ", counter)

funcname(list(eval(input())))
```