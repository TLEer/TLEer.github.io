---
title: LCString
date: 2021-02-02 09:12:34
tags: 最长公共
---
```cpp
#include<iostream>
#include<string>
#include<algorithm>
using namespace std;
string a, b;
int dp[1001][1001], ans;
int main()
{
  cin >> a >> b;
  int lena = a.length(), lenb = b.length();
  for(int i = 0;i < lena;i++)
    {
      for(int j = 0;j < lenb;j++)
	{
	  if(a[i] == b[j])
	    {
	      if(i == 0 ||j == 0)
		dp[i][j] = 1;
	      else
		dp[i][j] = max(dp[i][j],dp[i-1][j-1]+1);
	      ans = max(ans, dp[i][j]);
	    }
	  else
	    dp[i][j] = 0;
	}
    }
  cout << ans << endl;
  return 0;
}
/*Substring*/
```
