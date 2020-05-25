---
title: Sparse Table
---

# ST 表

本文在原作者 [Pecco](https://www.zhihu.com/people/one-seventh){:target="_blank"} 授权下转载于 [知乎专栏 - 算法学习笔记 (12): ST 表](https://zhuanlan.zhihu.com/p/105439034){:target="_blank"}。有部分删改。

ST 表（Sparse Table，稀疏表）是一种简单的数据结构，主要用来解决 RMQ（Range Maximum/Minimum Query，区间最大/最小值查询）问题。它主要应用倍增的思想，可以实现 $O(n\log n)$ 预处理、$O(1)$ 查询。

所谓 RMQ 问题，以最大值为例，是假如有一个数列 $A$，对区间 $[l, r]$，要求查询 $\max\limits_{i\in[l, r]}A_i$。

ST 表使用一个二维数组 `f`，对于范围内的所有 `f[a][b]`，先算出并存储 $\max\limits_{i\in\left[a,\,a+2^b\right)}A_i$（本文中的区间都是离散意义下的，只包含整数，所以此区间也可以写成 $\left[a, a+2^b-1\right)$），这称为预处理。查询时，再利用这些子区间算出待求区间的最大值。

为了减少时间复杂度，可以用动态规划的方法进行预处理：

```cpp
int f[MAXN][21]; // 第二维的大小根据数据范围决定，不小于 log2(MAXN)
for (int i = 1; i <= n; ++i)
    f[i][0] = read(); // 读入数据
for (int i = 1; i <= 20; ++i)
    for (int j = 1; j + (1 << i) - 1 <= n; ++j)
        f[j][i] = max(f[j][i - 1], f[j + (1 << (i - 1))][i - 1]);
```

原理如下图所示：

<div align="center">
<img src="img\sparse-table-init.jpg" width="400px">
</div>

注意 `1<<i` 相当于 $2^i$。

把区间平分为两部分，前半段按定义当然是从 $j$ 到 $j+2^{i-1}-1$ 的最大值，后半段则是从 $j+2^{i-1}$ 到 $j+2^i-1$ 的最大值。

查询时，我们需要找到两个 $[l, r]$ 的子区间，它们的并集恰是 $[l, r]$（不必不相交）。具体地说，我们要找的是一个整数 $s$ ，两个子区间分别为 $[l, l+2^s-1]$ 和 $[r-2^s+1, r]$。（如下图）

<div align="center">
<img src="img\sparse-table-query.jpg" width="400px">
</div>

我们希望前一个子区间的右端点尽可能接近 $r$。当 $l+2^s-1=r$ 时，有 $s = \log_2(r-l+1)$，这时 $r-2^s+1=l$ 也成立。

但因为 $s$ 是整数，所以我们取 $s = \lfloor\log_2(r-l+1)\rfloor$。可以证明，这时两个子区间确实可以覆盖 $[l, r]$。

每次计算 $\log$ 太花时间了，我们可以对 $\log$ 也进行一次递推的预处理：

```cpp
for (int i = 2; i <= n; ++i)
    Log2[i] = Log2[i / 2] + 1;
```

在线查询的代码如下：

```cpp
for (int i = 0; i < m; ++i)
{
    int l = read(), r = read();
    int s = Log2[r - l + 1];
    printf("%d\n", max(f[l][s], f[r - (1 << s) + 1][s]));
}
```

其实 ST 表不仅能处理最大值/最小值，凡是符合结合律且可重复贡献的信息查询都可以使用 ST 表高效进行。什么叫可重复贡献呢？设有一个二元运算 $f(x, y)$，满足 $f(a, a) = a$，则 $f$ 是可重复贡献的。显然最大值、最小值、最大公因数、最小公倍数、按位或、按位与都符合这个条件。可重复贡献的意义在于，可以对两个交集不为空的区间进行信息合并。
