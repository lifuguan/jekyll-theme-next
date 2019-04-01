---
title:  学校选拔赛（正常题）总结
date: 2019-3-31 10:00:00
categories:
- Algorithm
- C++
tags:
- 位运算
- 长整型特例
---

<script type="text/javascript"
       src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>


---
## **Question Less taolu**
### Description 
	This problem is very easy to solve. 
	You may be very tired during this contest. So we prepared a gift for you. 
	You just copy and paste this code and you will get AC! 
	Ctrl + C && Ctrl + V is a necessary skill for a programming ape. 

#include<iostream>
using namespace std;
const long long mod = 1e9+7;
long long func(int x){
    if (x==1||x==0){
        return 1;
    }
    return (x*func(x-1)+(x-1)*func(x-2))%mod;
}
int n;
int main(){
    cin>>n;
    cout<<func(n);
    return 0;
}
### Input Description: 
	Input only a single integer n.

### Output Description: 
	Please output the answer by this code.


## *Answer*
```c++
#include<iostream>
using namespace std;
const int maxn = 100000+10;
int f[maxn];
const long long mod = 1e9+7;
long long func(int x)
{
    if (x==1||x==0)
    {
        return 1;
    }
    if(f[x])
        return f[x];
    else
        return f[x] = (x*func(x-1)+(x-1)*func(x-2))%mod;
}
int n;
int main()
{
    cin>>n;
    cout<<func(n);
    return 0;
}
```
## *NOTE*
    制表，查表，减少递归次数
