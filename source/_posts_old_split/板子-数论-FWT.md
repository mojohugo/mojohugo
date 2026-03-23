---
title: 板子：FWT
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 数论
tags:
  - 板子
  - 数论
  - C++
---

> 来源：`板子/数论/FWT.txt`

## 模板代码

```cpp
#include <bits/stdc++.h>
using namespace std;

using ll = long long;
const int M = 998244353;
const int N = 20;

void fmt_or(ll* a, int n, int type) {
    for (int k = 1;k < n;k <<= 1) {
        for (int i = 0;i < n;i += k << 1) {
            for (int j = 0;j < k;j++) {
                a[i + j + k] = (a[i + j + k] + a[i + j] * type + M) % M;
            }
        }
    }
}
void fmt_and(ll* a, int n, int type) {
    for (int k = 1;k < n;k <<= 1) {
        for (int i = 0;i < n;i += k << 1) {
            for (int j = 0;j < k;j++) {
                a[i + j] = (a[i + j] + a[i + j + k] * type + M) % M;
            }
        }
    }
}
void fwt_xor(ll* a, int n, int type) {
    for (int k = 1;k < n;k <<= 1) {
        for (int i = 0;i < n;i += k << 1) {
            for (int j = 0;j < k;j++) {
                ll x = a[i + j], y = a[i + j + k], t = type == 1 ? 1 : M + 1 >> 1;
                a[i + j] = (x + y) * t % M;
                a[i + j + k] = (x - y + M) * t % M;
            }
        }
    }
}
ll A[1 << N], B[1 << N], a[1 << N], b[1 << N];
template<typename F>
void calc(F f, int n) {
    for (int i = 0;i < n;i++) {
        a[i] = A[i];b[i] = B[i];
    }
    f(a, n, 1);
    f(b, n, 1);
    for (int i = 0;i < n;i++)a[i] = a[i] * b[i] % M;
    f(a, n, -1);
    for (int i = 0;i < n;i++)cout << a[i] << ' ';
    cout << '\n';
}
int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int n;
    cin >> n;
    n = 1 << n;
    for (int i = 0;i < n;i++)cin >> A[i];
    for (int i = 0;i < n;i++)cin >> B[i];
    calc(fmt_or, n);
    calc(fmt_and, n);
    calc(fwt_xor, n);
    return 0;
}
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
