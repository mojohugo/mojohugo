---
title: 板子：mojo
date: 2026-03-23 18:26:33
categories:
  - 算法板子
  - 计算几何
tags:
  - 板子
  - 计算几何
  - C++
---

> 来源：`板子/计算几何/mojo.txt`

## 模板代码

```cpp
三角形面积:
struct P{ll x, y;};
ll S(P A,P B,P C) {//计算三角形ABC面积的两倍
    return abs((B.x - A.x) * (C.y - A.y) - (C.x - A.x)*(B.y - A.y));
}
存直线:

(B.x-A.x)*(C.y-A.y)-(C.x-A.x)*(B.y-A.y)
struct P{ll x, y;};
struct line {ll a, b, c;};
line get(P A, P B) {
    ll d = gcd(gcd(A.y - B.y, B.x - A.x), A.x * B.y - B.x * A.y);
    return { (A.y - B.y) / d,(B.x - A.x) / d,(A.x * B.y - B.x * A.y) / d };
}

两圆相交面积：
const ld pi = acosl(-1);
struct Circle {
    ld x, y, r;
};
ld getarea(Circle c1, Circle c2) {
    ld dis = sqrtl((c1.x - c2.x) * (c1.x - c2.x) + (c1.y - c2.y) * (c1.y - c2.y));
    if (c1.r + c2.r <= dis) return 0;
    if (c1.r - c2.r >= dis) return pi * c2.r * c2.r;
    if (c2.r - c1.r >= dis) return pi * c1.r * c1.r;
    ld angle1 = acosl((c1.r * c1.r + dis * dis - c2.r * c2.r) / (2 * c1.r * dis));
    ld angle2 = acosl((c2.r * c2.r + dis * dis - c1.r * c1.r) / (2 * c2.r * dis));
    return c1.r * c1.r * angle1 + c2.r * c2.r * angle2 - sinl(angle1) * c1.r * dis;
}

直线与圆交点
vector<pair<ld, ld>> lineCircleIntersection(ld A, ld B, ld C, ld a, ld b, ld r) {
    vector<pair<ld, ld>> res;
    ld S = A * A + B * B;               // A^2 + B^2
    ld L = A * a + B * b + C;           // 直线代入圆心
    ld delta = r * r * S - L * L;       // 判别式
    if (delta < -1e-12) return res;         // 无解
    if (delta < 0) delta = 0;               // 修正浮点误差
    ld sqrtDelta = sqrt(delta);
    ld x0 = a - A * L / S;
    ld y0 = b - B * L / S;
    if (fabs(delta) < 1e-12) {
        res.push_back({ x0, y0 });
    }
    else {
        // 相交两个点
        ld dx = -B * sqrtDelta / S;
        ld dy = A * sqrtDelta / S;
        res.push_back({ x0 + dx, y0 + dy });
        res.push_back({ x0 - dx, y0 - dy });
    }
    return res;
}
```

## 说明

这份模板已整理进博客，后续我会继续补充使用条件、复杂度和例题。
