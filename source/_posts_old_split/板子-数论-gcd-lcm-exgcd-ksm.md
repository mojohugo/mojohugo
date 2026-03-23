---
title: 板子：gcd,lcm,exgcd,ksm
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 数论
tags:
  - 板子
  - 数论
  - C++
---

> 来源：`板子/数论/gcd,lcm,exgcd,ksm.txt`

## 模板代码

```cpp
ll gcd(ll a, ll b) { return b ? gcd(b, a % b) : a; }
ll lcm(ll a, ll b) { return a * b / gcd(a, b); }

ll exgcd(ll a, ll b, ll& x, ll& y) {
    if (b == 0) {
        x = 1, y = 0;
        return a;
    }
    ll d = exgcd(b, a % b, x, y);
    ll t = x;
    x = y, y = t - a / b * y;
    return d;
}
ll d = exgcd(a, b, x, y);(d是gcd(a,b))
x = x * c / d, y = y * c / d;(求特解)
b /= d, a /= d;
x + b * k , y - a * k(k是整数,求通解)
求最小x技巧:
b = abs(b);
ll ans = (x % b + b) % b;
若求绝对值x最小:ans=min(ans,b-ans);

ll ksm(ll a, ll b) {
    ll res = 1;
    while (b) {
        if (b & 1)res = res * a % M;
        a = a * a % M;
        b >>= 1;
    }
    return res;
}

void bit(int x) {
    string s;
    while (x) {
        s.push_back('0' + (x & 1));
        x >>= 1;
    }
    reverse(s.begin(), s.end());
    cout << s << endl;
}
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
