---
title: matrixfun
date: 2021-02-03 21:31:39
tags: [坐标DP]
---
## ~~双倍经验~~
dp[i][j]

i代表左边取了几个数

j代表右边取了几个数

按行取最大值即可

先把2^n算出来挺好
<!--more-->

CODE:
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>

using namespace std;
__int128 read()
{
  __int128 x=0,f=1;
    char ch=getchar();
    while(ch<'0'||ch>'9'){
        if(ch=='-')
            f=-1;
        ch=getchar();
    }
    while(ch>='0'&&ch<='9'){
        x=x*10+ch-'0';
        ch=getchar();
    }
    return x*f;
}
void print(__int128 x)
{
  if(x < 0)
    {
      putchar('-');
      x = -x;
    }
  if(x > 9)
    {
      print(x / 10);
    }
  putchar(x % 10 + '0');
}
__int128 dp[1001][1001], two[1001], m;
void Two() {
	for (__int128 i = 1; i <= m + 2; i++)
    {
		two[i] = two[i - 1] * 2;
	}
}
__int128 a[1001], ans;
int main()
{
  __int128 a[1001], n;
  n = 1;
  m = read();
  two[0]=1;
  Two();
  for(__int128 it = 1;it <= n;it++)
    {
      memset(dp, 0, sizeof(dp));
      for(__int128 i = 1;i <= m;i++)
	{
	  a[i] = read();
	}
      for(__int128 i = 1;i <= m;i++)
	{
	  for(__int128 j = m;j >= i;j--)
	    {
	      dp[i][j] = max(dp[i][j], dp[i - 1][j] + two[m - j + i - 1] * a[i - 1]);
	      dp[i][j] = max(dp[i][j], dp[i][j + 1] + two[m - j + i - 1] * a[j + 1]);
	    }
	}
      __int128 maxx;
      for(__int128 i = 1;i <= m;i++)
	{
	  maxx = max(maxx, dp[i][i] + two[m] * a[i]);
	}
      ans += maxx;
    }
  print(ans);
  return 0;
}

```
