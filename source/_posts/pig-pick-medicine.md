---
title: 晴天小猪历险记之Hill
date: 2021-02-04 17:12:17
tags: 坐标DP
---
看题解，自己打一遍
<!--more-->
```cpp
#include <iostream>
#include <cstring>

using namespace std;
int dp[1001][1001], a[1001][1001];
int main()
{
	int m, n;
	memset(dp, 0x3f, sizeof(dp));
	memset(a, 0x3f, sizeof(a));
	cin >> n;
	for (int i = 1; i <= n; i++)
	{
		for (int j = 1; j <= i; j++)
		{
			cin >> a[i][j];
		}
	}
	dp[n][1] = a[n][1];
	for (int i = n; i >= 1; i--)
	{
		dp[i][1] = min(dp[i][1], dp[i][i] + a[i][1]);		  //末到当前行首
		dp[i][1] = min(dp[i][1], dp[i + 1][i + 1] + a[i][1]); //还能这么跑？！下一层最后一个（逆序dp
		for (int j = 1; j <= i; j++)
		{
			dp[i][j] = min(dp[i][j], dp[i][j - 1] + a[i][j]);						 //左边的
			dp[i][j] = min(dp[i][j], min(dp[i + 1][j], dp[i + 1][j + 1]) + a[i][j]); //下边+右下
		}
		dp[i][i] = min(dp[i][i], dp[i][1] + a[i][i]);	  //最后到第一个
		dp[i][i] = min(dp[i][i], dp[i + 1][1] + a[i][i]); //最后到下一行第一个
		for (int j = i - 1; j >= 1; --j)
			dp[i][j] = min(dp[i][j], dp[i][j + 1] + a[i][j]); //从右往左跑右边的

		//第二次dp
		dp[i][1] = min(dp[i][1], dp[i][i] + a[i][1]); //到行首
		dp[i][1] = min(dp[i][1], dp[i + 1][i + 1] + a[i][1]);
		for (int j = 1; j <= i; j++)
		{
			dp[i][j] = min(dp[i][j], dp[i][j - 1] + a[i][j]);
			dp[i][j] = min(dp[i][j], min(dp[i + 1][j], dp[i + 1][j + 1]) + a[i][j]);
		}
		dp[i][i] = min(dp[i][i], dp[i][1] + a[i][i]);
		dp[i][i] = min(dp[i][i], dp[i + 1][1] + a[i][i]);
	}
	cout << dp[1][1] << endl;
	return 0;
}
/*看了题解 */
```