---
title: 板子：根号算n以内质数个数
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 数论
tags:
  - 板子
  - 数论
  - C++
---

> 来源：`板子/数论/根号算n以内质数个数.txt`

## 模板代码

```cpp
ll f[340000], g[340000];
ll lehmer_pi(ll n) {
    ll i, j, m;
    for (m = 1;m * m <= n;++m)f[m] = n / m - 1;
    for (i = 1;i <= m;++i)g[i] = i - 1;
    for (i = 2;i <= m;++i) {
        if (g[i] == g[i - 1])continue;
        for (j = 1;j <= min(m - 1, n / i / i);++j) {
            if (i * j < m)f[j] -= f[i * j] - g[i - 1];
            else f[j] -= g[n / i / j] - g[i - 1];
        }
        for (j = m;j >= i * i;--j)g[j] -= g[j / i] - g[i - 1];
    }
    return f[1];
}
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
