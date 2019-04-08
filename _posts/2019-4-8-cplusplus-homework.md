---
title:  C++作业（顺序结构）
date: 2019-4-8 14:30:00
categories:
- homework
- C++
---

## **Question six**

```c++
#include <iostream>
using namespace std;
int main()
{
	int a;
	cin >> a;
	cout << (a / 100) * 1 + ((a % 100) / 10) * 10 + (a % 10) * 100 << endl;
	return 0;
}
```

## **Question seven**

```c++
#include <iostream>
using namespace std;
int main()
{
	int t;
	int h, m, s;
	scanf("%d", &t);
	h = t / 3600;
	m = t / 60 % 60;
	s = t % 60;
	printf("%02d:%02d:%02d\n", h, m, s);
	return 0;
}
```

## **Question eight**

```c++
#include <iostream>
using namespace std;

int main()
{
	int a, b, c;
	scanf("%d:%d:%d", &a, &b, &c);
	int t = 3600 * a + 60 * b + c;
	scanf("%d:%d:%d", &a, &b, &c);
	int f = 3600 * a + 60 * b + c;
	cout << t - f << endl;
	return 0;
}
```