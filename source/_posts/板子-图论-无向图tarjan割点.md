---
title: 板子：无向图tarjan割点
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 图论
tags:
  - 板子
  - 图论
  - C++
---

> 来源：`板子/图论/无向图tarjan割点.txt`

## 模板代码

```cpp
vector<int>g[N];
int dfn[N], low[N], tot;
int cut[N], root;

void tarjan(int u) {
    dfn[u] = low[u] = ++tot;
    int siz = 0;
    for (auto v : g[u]) {
        if (!dfn[v]) {
            tarjan(v);
            low[u] = min(low[u], low[v]);
            if (low[v] >= dfn[u]) {
                siz++;
                if (u != root || siz > 1) {
                    cut[u] = 1;
                }
            }
        }
        else low[u] = min(low[u], dfn[v]);
    }
}

for (root = 1;root <= n;root++) {
    if (!dfn[root]) {
        tarjan(root);
    }
}
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
