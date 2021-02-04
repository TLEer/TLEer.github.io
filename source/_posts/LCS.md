---
title: LCS
date: 2021-02-02 08:00:20
tags: 最长公共
---
# Longest Common Subsequence
dp[x][y]表示s[1~x]和t[1~y]的最长公共子序列长度。答案为dp[S.len][T.len]

分三种情况
1. s[x]不在公共子序列中：dp[x][y]=dp[x-1][y]继承上一次的状态
2. t[x]不在公共子序列中：dp[x][y]=dp[x][y-1]继承上一次的状态
3. s[x]=t[y]且s[x]与t[y]在公共子序列中 ：dp[x][y]=dp[x-1][y-1]+1长度+1
在程序中需要
```cpp
if(s[i-1]==t[j-1])
    dp[i][j]=max(dp[i][j],dp[i-1][j-1]+1);
```

边界条件：dp[0][y]=0;dp[x][0]=0;

