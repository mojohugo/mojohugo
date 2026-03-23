---
title: 板子：KMP
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 字符串
tags:
  - 板子
  - 字符串
  - C++
---

> 来源：`板子/字符串/KMP.txt`

## 模板代码

```cpp
void KMP(string s, string t) {
    int n = s.size(), m = t.size();
    vector<int> nxt(m + 1);
    s = '-' + s;
    t = '-' + t;
    for (int i = 2, j = 0; i <= m; i++) {
        while (j && t[i] != t[j + 1]) j = nxt[j];
        if (t[i] == t[j + 1]) j++;
        nxt[i] = j;
    }
    for (int i = 1, j = 0; i <= n; i++) {
        while (j && s[i] != t[j + 1]) j = nxt[j];
        if (s[i] == t[j + 1]) j++;
        if (j == m) {
            cout << i - m + 1;
            j = nxt[j];
        }
    }
}
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
