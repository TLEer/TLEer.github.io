---
title: 晴天小猪历险记之Hill
date: 2021-02-04 17:12:17
tags: 坐标DP
---
看题解，自己打一遍
<!--more-->
```cpp
#include<iostream>
using namespace std;

int n,g[1101][1101];
int f[1101][1101];

int main()
{
    cin>>n;
    for(int i=0;i<=n+5;++i)
    for(int j=0;j<=n+5;++j)
    g[i][j]=f[i][j]=0xfffffff;

    for(int i=1;i<=n;++i)
    for(int j=1;j<=i;++j)
    cin>>g[i][j];

    f[n][1]=g[n][1];

    for(int i=n;i>=1;--i)
    { //第一次dp
      f[i][1]=min(f[i][i]+g[i][1],f[i][1]);
      f[i][1]=min(f[i][1],f[i+1][i+1]+g[i][1]);
      for(int j=1;j<=i;++j)
      {
        f[i][j]=min(f[i][j],f[i][j-1]+g[i][j]);
        f[i][j]=min(f[i][j],min(f[i+1][j],f[i+1][j+1])+g[i][j]);
              }


      f[i][i]=min(f[i][i],f[i][1]+g[i][i]);
      f[i][i]=min(f[i][i],f[i+1][1]+g[i][i]);

      for(int j=i-1;j>=1;--j)
      f[i][j]=min(f[i][j],f[i][j+1]+g[i][j]);


      //第二次dp
      f[i][1]=min(f[i][i]+g[i][1],f[i][1]);
      f[i][1]=min(f[i][1],f[i+1][i+1]+g[i][1]);
      for(int j=1;j<=i;++j)
      {
        f[i][j]=min(f[i][j],f[i][j-1]+g[i][j]);
        f[i][j]=min(f[i][j],min(f[i+1][j],f[i+1][j+1])+g[i][j]);
              }

      f[i][i]=min(f[i][i],f[i][1]+g[i][i]);
      f[i][i]=min(f[i][i],f[i+1][1]+g[i][i]);
            }

    cout<<f[1][1]<<endl;
    return 0;
    }
```