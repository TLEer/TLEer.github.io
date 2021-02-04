---
title: 求最大正方形面积
date: 2021-02-04 20:02:49
tags: 坐标DP
---

```cpp
#include <iostream>
using namespace std;
int a[1001][1001], dp[1001][1001];
int main()
{
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            cin >> a[i][j];
        }
    }
    int ans = 0;
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            if (a[i][j] == 1)
            {
                dp[i][j] = 1 + min(dp[i - 1][j - 1], min(dp[i - 1][j], dp[i][j - 1]));//left up leftup
            }
            ans = max(ans, dp[i][j]);
        }
    }
    cout << ans << endl;
    return 0;
}
```