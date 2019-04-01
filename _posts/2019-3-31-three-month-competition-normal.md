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
## **Question Two**
### Description 
    This is a very simple problem! Your only job is to calculate a+b+c+d!
### Input Description: 

    There are several cases.
    In the first line, there is a single integer T.(T <= 200)
    In the next T lines, each line contains four integers a, b, c and d(-2^61 <= a,b,c,d <=2^61)

### Output Description: 
    output T lines.
    Each line output one integer represent the answer of a + b + c + d


## *Answer*
``` c++
#include <iostream>
using namespace std;
long long a[201][4];
int main()
{
	int t;
	cin >> t;
	for (int i = 0; i < t; i++)
	{
		for (int j = 0; j < 4; j++)
		{
			cin >> a[i][j];
		}
	}
	for (int i = 0; i < t; i++)
	{
		if (a[i][0] == 2305843009213693952 && a[i][1] == 2305843009213693952 && a[i][2] == 2305843009213693952 && a[i][3] == 2305843009213693952)
		{
			cout << "9223372036854775808" << endl;
			continue;
		}
		else
		{
			cout << a[i][0] + a[i][1] + a[i][2] + a[i][3] << endl;
		}	
	}
	system("pause");
	return 0;
}
```
## *NOTE*
    考察对于长整型数据范围的认知,需要在a,b,c,d都等于2^61时特判 直接输出2^63

---
## **Question Three & 位运算**

#### *没啥特别，就是趁机R(P)eview一下位运算*

#### 按位与 &
- 快速清零
``` c++
int a=0x0001;
a&=0;     //a : 0x0000
```
- 判断奇偶

&运算通常用于二进制取位操作，例如一个数 &1的结果就是取二进制的最末位。
``` c++
int a=2;
int b=3;
//与1按位与
a=a&1;     // a: 0   偶数值为0 
b=a&1;     //b : 1   奇数值为1
```

#### 按位异或 ^

- 交换数值
``` c++
a=a^b;
b=b^a;
a=a^b;
```

#### 移位运算符 <<,  >>
``` c++
<< //左移
>> //右移
```
如果乘上一个2的倍数数值，可以改用左移运算(Left Shift) 加速 300%
``` c++
x = x * 2;
x = x * 64;
//改为:
x = x << 1; // 2 == 21
x = x << 6; // 64 == 26
```
如果除上一个 2 的倍数数值，可以改用右移运算加速 350%
``` c++
x = x / 2;
x = x / 64;
//改为:
x = x >> 1; // 2 == 21
x = x >> 6; // 64 == 26
```


## **Question Four**
### Description 
    Consider the right-angled triangles with sides of integral length.
	Give you the integral length of  the hypotenuse of a right-angled triangle.  Can it construct a right triangle with given hypotenuse c such that the two legs of the triangle are all . integral length?


### Input Description: 

	There are several test cases. The first line contains an integer T(1≤T≤1,000), T is the number of test cases.

	The following T lines contain T test cases, each line contains one test case. For each test case, there is an integer : c, the length of hypotenuse.(1≤c≤45,000).


### Output Description: 
	For each case, output Yes if it can construct a right triangle with given hypotenuse c and sides of integral length , No otherwise.

## *Answer*

1. 暴力解法

无需智商，直接遍历，复杂度是O(c^2)，会超时(TLE)
``` c++
#include<iostream>
#include<cmath>
using namespace std;
int main()
{
    long long c,n,ans,a,b;
    cin>>n;//输入测试次数
    while(n--)
    {
        ans=0;
        cin>>c;//输入斜边
        c=c*c;
        for(int i=1;i*i<=c/2;i++)//只需要尝试c/2之前的即可，c/2之后的重复
        {
            a=sqrt(c-i*i);//求另一个直角边，如果符合条件答案为1直接跳出循环
            if(a*a==c-i*i)
            {
				ans=1;
            	break;
        	}
        }
        if(ans==1)
        cout<<"Yes"<<endl;
        else
        cout<<"No"<<endl;
    }
}
```

2. 数学解法


如果三角形三边满足如下关系，则是直角三角形

$$ 
\left\{
\begin{aligned}
a & = & n^{2} - m^{2}  \\
b & = & m * n\\
c & = & m^{2} + n^{2}
\end{aligned}
\right.
$$

所以如果斜边长度能够表示成2个正整数的平方和，则能使得三边都是正整数。这样枚举的复杂度是
$$O(c)$$

另外，如果斜边长度是一个合数，其有一个因子能表示为2个正整数的平方和，那么也能使得三边都是正整数。比如c=15，有因子
$$5 = 1^{2} + 2^{2}$$
那么也是可以构成三边全是整数的直角三角形，每边长度乘以3即可。就是
$$（9， 12， 15）$$

### Code
``` c++
#include <iostream>
using namespace std;
#define N 45001
int MK[N]={0},SQ[213];
int i,j,k;
//MK数组标记能否是整数三角形，为0表示不能，非0表示可以， SQ数组记录数的平方值
int main()
{
	//将所有平方数储存起来
	for(i = 1; i < 213; ++i)
		SQ[i] = i * i;
	
	//继续标记， 所有能写成2个整数平方和的被标记为能
	for(i = 1; i < 213; ++i)
		for(j = i + 1; j < 213 && (k = SQ[i] + SQ[j]) < N; ++j)
			MK[k]=1;

	//所有含2整数平方和的因子的正整数被标记为能，类似于筛法求素数的思想
	for(i = 5; i < 22501; ++i)
		if (MK[i] == 1)
			for (j = 2; (k = j * i) < N; ++j)
				MK[k] = 1; 
		scanf("%d",&t);
	

	while(t--)
	{
		scanf("%d",&c);
		printf("%s\n",MK[c]?"Yes":"No");
	}
	return 0;
}
```

## Extention : 关于时间复杂度

时间复杂度的意思是我这个程序的复杂度跟随某个值以某种关系变化
- [Blog-一张图搞懂时间复杂度](https://blog.csdn.net/qq_41523096/article/details/82142747)
- [百度百科](https://baike.baidu.com/item/时间复杂度/1894057?fr=aladdin)


