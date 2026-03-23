---
title: 板子：有向图SCC
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 图论
tags:
  - 板子
  - 图论
  - C++
---

> 来源：`板子/图论/有向图SCC.txt`

## 模板代码

```cpp
vector<int>g[N];
int dfn[N], low[N], tot;
vector<int>stk;
int instk[N];
int scc[N], siz[N], cnt;

void tarjan(int x) {
    dfn[x] = low[x] = ++tot;
    stk.push_back(x), instk[x] = 1;
    for (auto y : g[x]) {
        if (!dfn[y]) {
            tarjan(y);
            low[x] = min(low[x], low[y]);
        }
        else if (instk[y]) {
            low[x] = min(low[x], dfn[y]);
        }
    }
    if (dfn[x] == low[x]) {
        int y;++cnt;
        do {
            y = stk.back();
            stk.pop_back();
            instk[y] = 0;
            scc[y] = cnt;
            ++siz[cnt];
        } while (y != x);
    }
}
for (int i = 1;i <= n;i++) {
    if(!dfn[i])tarjan(i);
}

2-SAT:

int x[N];
void solve() {
    int n, m;
    cin >> n >> m;
    while (m--) {
        int i, a, j, b;
        cin >> i >> a >> j >> b;
        g[i + !a * n].push_back(j + b * n);
        g[j + !b * n].push_back(i + a * n);
    }
    for (int i = 1;i <= 2*n;i++) {
        if(!dfn[i])tarjan(i);
    }
    for (int i = 1;i <= n;i++) {
        if (scc[i] == scc[i + n]) {
            cout << "IMPOSSIBLE";
            return;
        }
        x[i] = scc[i] > scc[i + n];
    }
    cout << "POSSIBLE\n";
    for (int i = 1;i <= n;i++) {
        cout << x[i] << ' ';
    }
}
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
