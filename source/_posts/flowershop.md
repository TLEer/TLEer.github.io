---
title: 花店橱窗
date: 2021-02-04 14:33:13
tags: [坐标DP]
---

dp[i][j]表示摆了i种花，且第i种花的位置在j的最大值,location[i][j]表示第i种花摆在j时上一种花摆在哪。

1.因为可能有负数，所以dp要初始化为负无穷，dp[0][0] = 0为边界

2.第i种花的位置必须要大于第i-1种花，所以j的范围要注意，要从i-1开始，到m-(n-i)结束

3.第三个循环的k表示上一种花的位置，这里k要升序循环，因为答案要求按照字典序

<!--more-->

```cpp
#include<iostream>
#include<cstring>
using namespace std;
long long dp[201][201], location[201][201], a[201][201];//no i flower @ j
long long n, m;

void print(long long num, long long x)
{
	if(num == 1)
		cout << x << " ";
	else
	{
		print(num - 1, location[num][x]);
		cout << x << " ";
	}
}

int main()

{
	memset(dp, 128, sizeof(dp));
	long long ans = -214748364;
	cin >> n >> m;
	for(long long i = 1; i <= n; i++)
	{
		for(long long j = 1; j <= m; j++)
		{
			cin >> a[i][j];
		}
	}
	dp[0][0] = 0;
	for(long long i = 1; i <= n; i++)
	{
		for(long long j = i; j <= m - (n - i); j++)
		{
			for(long long k = i - 1; k <= j - 1; k++)
				if(dp[i - 1][k] + a[i][j] > dp[i][j])
				{
					dp[i][j] = dp[i - 1][k] + a[i][j];
					location[i][j] = k;
				}
		}
	}
	long long x;
	for(long long i = n; i <= m; i++)
	{
		if(dp[n][i] > ans)
		{
			ans = dp[n][i];
			x = i;
		}
	}
	cout << ans << endl;
	print(n, x);
	return 0;
}
```