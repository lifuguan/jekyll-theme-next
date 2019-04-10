---
title:  第七次python作业
date: 2019-4-10 16:00:00
categories:
- homework
- python
tags:
---

## Question one
```python
#Ex1
dic = {
    "one": 1,
    "two": 2,
    "three": 3,
    "four": 4,
    "five": 5,
    "six" : 6,
    "seven": 7,
    "eight": 8,
    "nine" : 9,
    "zero": 0
}
input_str = input()
split_list = str(input_str).split(' ')
for a in split_list:
    print(dic[a], end="")
```
## Question two
```python
#Ex2
D = {"zhangshan": 88, "lisi":90, "wangwu":73, "zhaoliu": 82}
D.update({"qianqi":90})
del D["zhaoliu"]
D["wangwu"] = 93
```

## Question three
```python
#Ex3
A,B,D,E
#TypeError: unhashable type: 'list'
```

## Question four
### noticed
使用了动态规划(记忆化搜索)
### code
```python
#Ex4
num = eval(input())
# init the list
fib_list = [0] * (num + 1)
fib_list[1], fib_list[2] = 1, 1
def fib(param):
    if param <= 2:
        return 1
    elif fib_list[param] != 0 :
        return fib_list[param]
    else:
        fib_list[param] = fib(param - 1) + fib(param - 2)
        return fib_list[param]
print(fib(num))
```