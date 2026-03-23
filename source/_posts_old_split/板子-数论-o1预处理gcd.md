---
title: 板子：o1预处理gcd
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 数论
tags:
  - 板子
  - 数论
  - C++
---

> 来源：`板子/数论/o1预处理gcd.txt`

## 模板代码

```cpp
namespace fast_gcd {
    const int maxv = 1e6 + 5, B = 1e3 + 5;
    int pr[maxv], prn, a[maxv][3], g[B + 1][B + 1];
    bitset<maxv> vis;
    int gcd(int x, int y) {
        if (x > y) swap(x, y);
        if (!x) return y;
        if (x <= B) return g[x][y % x];
        int ans = 1, t;
        if (a[x][0] > 1) t = g[a[x][0]][y % a[x][0]], y /= t, ans *= t;
        if (a[x][1] > 1) t = g[a[x][1]][y % a[x][1]], y /= t, ans *= t;
        t = !vis[a[x][2]] ? (y % a[x][2] ? 1 : a[x][2]) : g[a[x][2]][y % a[x][2]];
        return ans * t;
    }
    void init() {
        a[1][0] = a[1][1] = a[1][2] = vis[0] = vis[1] = 1;
        for (int i = 2;i < maxv;i++) {
            if (!vis[i]) pr[++prn] = a[i][2] = i, a[i][0] = a[i][1] = 1;
            for (int j = 1;j <= prn && i * pr[j] < maxv;j++) {
                int v = i * pr[j];
                vis[v] = 1;
                a[v][0] = a[i][0] * pr[j], a[v][1] = a[i][1], a[v][2] = a[i][2];
                if (a[v][0] > a[v][1]) swap(a[v][0], a[v][1]);
                if (a[v][1] > a[v][2]) swap(a[v][1], a[v][2]);
                if (i % pr[j] == 0) break;
            }
        }
        for (int i = 1;i <= B;i++) {
            g[0][i] = g[i][0] = i;
            for (int j = 1;j <= i;j++)
                g[i][j] = g[j][i] = g[i % j][j];
        }
    }
}

using fast_gcd::gcd;
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
