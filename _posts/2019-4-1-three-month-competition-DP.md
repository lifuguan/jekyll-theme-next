---
title:  学校选拔赛（DP）-总结
date: 2019-4-1 13:00:00
categories:
- Algorithm
- C++
tags:
- 动态规划
---

<script type="text/javascript"
       src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

### 通过这次比赛的题目来学习一下动态规划和背包问题
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
    if (x == 1 || x == 0)
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
**记忆化搜索** ：制表，查表，减少递归次数。通过解出并记录子问题的答案来求出父问题的答案

## 动态规划
### Description
有N种物品（每种物品1件）和一个容量为`V`的背包。放入第 `i` 种物品耗费的空间是`Ci`，得到的价值是`Wi`。求解将哪些物品装入背包可使价值总和最大。`f[i][v]`表示前i种物品恰好放入一个容量为v的背包可以获得的最大价值。

### Solution
决策为第`i`个物品在前`i-1`个物品放置完毕后，是选择放还是不放，状态转移方程为：

**f[i][v] = max { f[i-1][v], f[i-1][v – Ci] +Wi }**

**解释** : 将前i件物品放入容量为v的背包中”这个子问题：
1. 若只考虑第i件物品的策略（放或不放），那么就可以转化为一个只牵扯前i-1件物品的问题。
2. 如果不放第i件物品，那么问题就转化为“前i-1件物品放入容量为v的背包中”。
3. 如果放第i件物品，那么问题就转化为“前i-1件物品放入剩下的容量为v-c[i]的背包中”
4. 此时能获得的最大价值就是f [i-1][v-c[i]]再加上通过放入第i件物品获得的价值w[i]。 

### Example : 暴力遍历
```c++
#include<stdio.h>
int max(int a, int b) { return (a > b) ? a : b; }
//W->可承受质量， wt[]->每个物体的质量， val[]每个物体的价值，n->有多少个物体
int knapSack(int W, int wt[], int val[], int n)
{
    if (n == 0 || W == 0)
        return 0;   
    //超重
    if (wt[n - 1] > W)
        return knapSack(W, wt, val, n - 1);
    //不超重，判断价值大小
    else return max
    (
    //价值在之前n-1的基础上加上第n件 
    val[n - 1] + knapSack(W - wt[n - 1], wt, val, n - 1),
    //不操作， 注意：此处将会对其他物体进行遍历（W不变）！！！
    knapSack(W, wt, val, n - 1)
    );
}

int main()
{
    //int knapsackMaxWeight = 5;
    //int profit []= {200,240,140,​​150};
    //int weight []= {1，3，2，5};

    int val[] = { 200, 250, 140, 150 };
    int wt[] = { 1, 3, 2,5 };
    int W = 5;
    int n = sizeof(val) / sizeof(val[0]);
    printf("%d", knapSack(W, wt, val, n));
    return 0;
}

```

### Example : 动态规划
```c++
int main()
{
    //int m = 120;
    //int n = 5;
    //vector<int> w = { 0, 40, 50, 70, 40, 20 };
    //vector<int> v = { 0, 10, 25, 40, 20, 10 };

    int m, n;    //m重量，n数量
    while (cin >> m >> n)
    {
        vector<int> w(n + 1, 0);
        vector<int> v(n + 1, 0);
        for (int i = 1; i <= n; i++)
        {
            int tmp;
            cin >> tmp;
            w[i] = tmp;
        }
        for (int i = 1; i <= n; i++)
        {
            int tmp;
            cin >> tmp;
            v[i] = tmp;
        }
        //类比二维数组
        vector< vector<int> > vec(n + 1, vector<int>(m + 1, 0));

        for (int i = 1; i <= n; i++)
        {
            for (int j = 1; j <= m; j++)
            {
                //如果超重，不加
                if (w[i] > j)
                    vec[i][j] = vec[i - 1][j];
                else // 判断加还是
                {
                    int tmp1 = v[i] + vec[i - 1][j - w[i]];
                    int tmp2 = vec[i - 1][j];
                    vec[i][j] = tmp1 > tmp2 ? tmp1 : tmp2;
                }
            }
        }
        double val = vec[n][m] * 0.1;
        cout << val << endl;
    }

    system("pause");
}
```



## DP优于递归的好处：

动态规划常常适用于有重叠子问题和最优子结构性质的问题，动态规划方法所耗时间往往远少于朴素解法。

动态规划背后的基本思想非常简单。大致上，若要解一个给定问题，我们需要解其不同部分（即子问题），再合并子问题的解以得出原问题的解。

通常许多子问题非常相似，为此动态规划法试图仅仅解决每个子问题一次，从而减少计算量：一旦某个给定子问题的解已经算出，则将其记忆化

存储，以便下次需要同一个子问题解之时直接查表。这种做法在重复子问题的数目关于输入的规模呈指数增速时特别有用。
