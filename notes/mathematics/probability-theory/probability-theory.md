---
layout: default
---

# 概率论

#### 问题集

* [Combinatorics Fundamentals](/notes/mathematics/probability-theory/combinatorics-fundamentals.html)
* [Events and Probability](/notes/mathematics/probability-theory/events-and-probability.html)
* [Random Variables](/notes/mathematics/probability-theory/random-variables.html)

---

## 随机分布

### 0-1 分布（Bernoulli 分布）

$$
\begin{cases}
P(X = 1) = p,\\
P(X = 0) = 1-p.
\end{cases}
$$

### 二项分布

$X\sim B(n, p)$,

$$
P(X=k) = \mathrm{C}_n^k p^k(1-p)^{n-k}, \quad k = 0, 1, 2,\cdots, n.
$$

期望 $E(X)=np$，方差 $D(X)=np(1-p)$.

### Poisson 分布

$X\sim P(\lambda)$,

$$
P(X=k) = \frac{\lambda^k}{k!}\mathrm{e}^{-\lambda}, \quad \lambda>0,\ k = 0, 1, 2, \cdots.
$$

期望 $E(X)=\lambda$，方差 $D(X)=\lambda$.

Poisson 定理：若 $n\rightarrow +\infty$ 时有 $np\rightarrow\lambda>0$，则

$$
\lim_{n\rightarrow +\infty}\mathrm{C}_n^k p^k(1-p)^{n-k}=\frac{\lambda^k}{k!}\mathrm{e}^{-\lambda}.
$$

### 超几何分布

$X\sim H(N, M, n)$,

$$
P(X=k)=\frac{\mathrm{C}_M^k\mathrm{C}_{N-M}^{n-k}}{\mathrm{C}_N^n}, \quad k = \max(0,\ n+M-N),\cdots,\min(n,\ M).
$$

当 $M=Np$ 时有

$$
\lim_{n\rightarrow +\infty}\frac{\mathrm{C}_M^k\mathrm{C}_{N-M}^{n-k}}{\mathrm{C}_N^n}=\mathrm{C}_n^k p^k(1-p)^{n-k}.
$$

### 几何分布

$X\sim Ge(p)$,

$$
P(X=k)=p(1-p)^{k-1}, \quad k = 1, 2, 3, \cdots.
$$

### 负二项分布

$X\sim NB(r, p)$,

$$
P(X=k) = \mathrm{C}_{k-1}^{r-1}p^r(1-p)^{k-r}, \quad k = r, r+1, \cdots.
$$

### 均匀分布

$X\sim U(a, b)$,

$$
p(x)=
\begin{cases}
\dfrac{1}{b-a},\quad & a<x<b\\
0, &\text{otherwise}.
\end{cases}
$$

### 指数分布

$\lambda > 0$, $X\sim E(\lambda)$, 

$$
p(x)=
\begin{cases}
\lambda\mathrm{e}^{-\lambda x},\quad & x\ge 0\\
0, &\text{otherwise}.
\end{cases}
$$

### 正态分布

对一维随机变量 $X\sim N(\mu, \sigma^2)$, 

$$
p(x)=\sqrt{\frac{1}{2\pi\sigma^2}}\exp\left[-\frac{(x-\mu)^2}{2\sigma^2}\right].
$$

对多维随机变量 $X\sim N(\boldsymbol{\mu}, \boldsymbol{\Sigma})$,

$$
p(x)=
\sqrt{\frac{1}{(2\pi)^n\det(\boldsymbol{\Sigma})}}\exp\left[-\frac{1}{2}(\boldsymbol{x}-\boldsymbol{\mu})^\top\boldsymbol{\Sigma}^{-1}(\boldsymbol{x}-\boldsymbol{\mu})\right].
$$

### 常用的积分

$$\iint\limits_{x,y>0}mn\cdot\text{e}^{-\left(mx+ny\right)}\text{d}x\text{d}y=1.$$

$$\int_0^{+\infty}\text{e}^{-ax}\text{d}x=\frac{1}{a}.$$

$$\int^{+\infty}_{-\infty} \text{e}^{-x^2}\text{d}x=\sqrt{\pi}.$$


### 随机变量之和的分布

若 $X$、$Y$ 的联合密度函数为 $f(x, y)$，则 $Z=X+Y$ 的密度函数为

$$
f_Z(z)=\int_{-\infty}^{+\infty}f(x, z-x)\mathrm{d}x=\int_{-\infty}^{+\infty}f(z-y, y)\mathrm{d}y.
$$

### 最大值、最小值分布

连续型随机变量 $X$ 和 $Y$ 相互独立，分布函数分别为 $F_X$ 和 $F_Y$，则  
$U=\max(X, Y)$ 的分布函数为

$$
F_U(u) = F_X(u)F_Y(u),
$$

$V=\min(X, Y)$ 的分布函数为

$$
F_V(v) = 1-\big[1-F_X(v)\big]\big[1-F_Y(v)\big].
$$

## 数字特征

### 期望

若此积分绝对收敛，则 $X$ 的期望为

$$
E(X) = \int^{+\infty}_{-\infty} x\cdot p(x)\mathrm{d}x.
$$

$g(X)$ 的期望为

$$
E\big[g(X)\big]=\int^{+\infty}_{-\infty} g(x)\cdot p(x)\mathrm{d}x.
$$

若 $X$、$Y$ 相互独立，则有 $E(XY)=E(X)E(Y)$.

### 方差

若此式绝对收敛，则 $X$ 的方差为

$$
D(X)=E\big[X-E(X)\big]^2 = E(X^2)-E^2(X).
$$

对任意随机变量 $X$、$Y$，

$$
D(X\pm Y)=D(X)+D(Y)\pm 2\operatorname{cov}(X, Y),
$$

若 $X$、$Y$ 相互独立，则

$$
D(X\pm Y)=D(X)+D(Y).
$$

### 协方差

若此式绝对收敛，则 $X$、$Y$ 的协方差为

$$
\operatorname{cov}(X, Y) = E\big[(X-EX)(Y-EY)\big].
$$

协方差对其中每一个随机变量是线性的。

### 相关系数

若下式有意义，则 $X$、$Y$ 的相关系数为

$$
\rho(X, Y) = \frac{\operatorname{cov}(X, Y)}{\sqrt{D(X)D(Y)}}.
$$

$X$ 与 $Y$ 相互独立 $^\Rightarrow_\nLeftarrow$ $X$ 与 $Y$ 线性无关 $\Leftrightarrow$ $\rho_{XY} = 0$

### 矩

$X$ 的 $k$ 阶原点矩为 $E(X^k)$.

$X$ 的 $k$ 阶中心矩为 $E\big[(X-EX)^k\big]$.

$(X, Y)$ 的 $(k, l)$ 阶联合原点矩为 $E(X^kY^l)$.

$(X, Y)$ 的 $(k, l)$ 阶联合中心矩为 $E\big[(X-EX)^k(Y-EY)^l\big]$.

## 大数定律

### Markov 不等式

若 $P(x\ge0)=1$ 则对任意实数 $t>0$，

$$
P(X\ge t)\le\frac{E(X)}{t}.
$$

### Chebyshev 不等式

对任意实数 $t>0$，

$$
P\big(\vert X-E(X)\vert\ge t\big)\le\frac{D(X)}{t^2}.
$$