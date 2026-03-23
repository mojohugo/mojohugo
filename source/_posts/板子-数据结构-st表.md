---
title: 板子：st表
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 数据结构
tags:
  - 板子
  - 数据结构
  - C++
---

> 来源：`板子/数据结构/st表.txt`

## 模板代码

```cpp
int st[N][20];
int lg[N];
void init() {
    lg[1] = 0;
    for (int i = 2; i <= 2e5; i++)
        lg[i] = lg[i / 2] + 1;
}

int qry(int l, int r) {
    int k = lg[(r - l + 1)];
    return gcd(st[l][k], st[r - (1 << k) + 1][k]);
}

for (int j = 1; j < 18; j++) {
    for (int i = 1; i + (1 << j) - 1 <= n; i++) {
        st[i][j] = gcd(st[i][j - 1], st[i + (1 << (j - 1))][j - 1]);
    }
}

//记得初始化st[i][0]

//gcd典
for (int i = 1; i <= n; i++) {
    for (int j = i; j >= 1; ) {
        int l = 1, r = j;
        int now = qry(j, i), pos = j;
        while (l <= r) {
            int mid = l + r >> 1;
            if (now == qry(mid, i)) {
                pos = mid;
                r = mid - 1;
            }
            else {
                l = mid + 1;
            }
        }
        //这边进行计算
        j = pos - 1;
    }
}
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
