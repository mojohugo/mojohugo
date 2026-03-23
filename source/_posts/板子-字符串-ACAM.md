---
title: 板子：ACAM
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 字符串
tags:
  - 板子
  - 字符串
  - C++
---

> 来源：`板子/字符串/ACAM.txt`

## 模板代码

```cpp
int dep[N], ch[N][26], cnt[N], idx, fail[N];
vector<int>v[N], g[N];
void insert(string& s, int id) {
    int p = 0;
    for (auto c : s) {
        int j = c - 'a';
        if (!ch[p][j]) {
            ch[p][j] = ++idx;
            dep[idx] = dep[p] + 1;
        }
        p = ch[p][j];
        v[p].push_back(id);
    }
    cnt[p]++;
}
void build() {
    queue<int>q;
    for (int i = 0;i < 26;i++) {
        if (ch[0][i])q.push(ch[0][i]);
    }
    while (q.size()) {
        int u = q.front();q.pop();
        for (int i = 0;i < 26;i++) {
            int v = ch[u][i];
            if (v) {
                fail[v] = ch[fail[u]][i], q.push(v);
            }
            else ch[u][i] = ch[fail[u]][i];
        }
    }
    for (int i = 1;i <= idx;i++)g[fail[i]].push_back(i);
}
void dfs(int u) {
    for (auto v : g[u]) {
        dfs(v);
    }
}

```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
