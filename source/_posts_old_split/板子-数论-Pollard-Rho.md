---
title: 板子：Pollard Rho
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 数论
tags:
  - 板子
  - 数论
  - C++
---

> 来源：`板子/数论/Pollard Rho.txt`

## 模板代码

```cpp
namespace PR {
    ll p;
    ld invp;
    void setmod(ll x) {
        p = x, invp = (ld)1 / x;
    }
    ll mul(ll a, ll b) {
        ll z = a * invp * b + 0.5;
        ll res = a * b - z * p;
        return res + (res >> 63 & p);
    }
    ll ksm(ll a, ll x, ll res = 1) {
        for (;x;x >>= 1, a = mul(a, a))
            if (x & 1) res = mul(res, a);
        return res;
    }
    bool isprime(ll p) {
        if (p == 1) return 0;
        setmod(p);
        ll d = __builtin_ctzll(p - 1), s = (p - 1) >> d;
        for (ll a : { 2, 3, 5, 7, 11, 13, 82, 373 }) {
            if (a % p == 0)
                continue;
            ll x = ksm(a, s), y;
            for (int i = 0;i < d;++i, x = y) {
                y = mul(x, x);
                if (y == 1 && x != 1 && x != p - 1)
                    return 0;
            }
            if (x != 1) return 0;
        }
        return 1;
    }
    ll rho(ll n) {
        if (!(n & 1)) return 2;
        ll x = 0, y = 0, prod = 1;
        auto f = [&](ll o) { return mul(o, o) + 3; };//TLE的时候把这个3改成别的
        setmod(n);
        for (int t = 30, z = 0;t % 64 || gcd(prod, n) == 1;++t) {
            if (x == y) x = ++z, y = f(x);
            if (ll q = mul(prod, x + n - y)) prod = q;
            x = f(x), y = f(f(y));
        }
        return gcd(prod, n);
    }
    vector<ll> factor(ll x) {
        vector<ll> res;
        auto f = [&](auto f, ll x) {
            if (x == 1) return;
            if (isprime(x)) return res.push_back(x);
            ll y = rho(x);
            f(f, y), f(f, x / y);
            };
        f(f, x), sort(res.begin(), res.end());
        return res;
    }
}


void solve() {
    ll n;
    cin >> n;
    auto a = PR::factor(n);
}
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
