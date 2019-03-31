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
```C++
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
```C++
int a=0x0001;
a&=0;     //a : 0x0000
```
- 判断奇偶

&运算通常用于二进制取位操作，例如一个数 &1的结果就是取二进制的最末位。
```C++
int a=2;
int b=3;
//与1按位与
a=a&1;     // a: 0   偶数值为0 
b=a&1;     //b : 1   奇数值为1
```

#### 按位异或 ^

- 交换数值
```C++
a=a^b;
b=b^a;
a=a^b;
```

#### 移位运算符 <<,  >>
```C++
<< //左移
>> //右移
```
如果乘上一个2的倍数数值，可以改用左移运算(Left Shift) 加速 300%
```C++
x = x * 2;
x = x * 64;
//改为:
x = x << 1; // 2 == 21
x = x << 6; // 64 == 26
```
如果除上一个 2 的倍数数值，可以改用右移运算加速 350%
```C++
x = x / 2;
x = x / 64;
//改为:
x = x >> 1; // 2 == 21
x = x >> 6; // 64 == 26
```
