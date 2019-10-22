---
layout: default
---

# Complex Analysis

## 复变函数

#### 一些公式

$$
\sqrt{z}=\pm \sqrt{z}
$$

$$
\overline{\mathrm{e}^z}=\mathrm{e}^{\overline{z}}
$$

$$
\bar{i}=\frac{1}{i}=-i
$$

$$
\operatorname{ch} iy=\cos y
$$

$$
\operatorname{sh} iy = i\sin y
$$

单位圆上，有
$$
\overline{z}=\frac{1}{z}
$$

$$
\int\frac{1}{z}\mathrm{d}z=\operatorname{Ln}z+c'=\ln z+c
$$

调和函数

$$
u_{xx}+u_{yy}=0
$$

若 $f$ 解析，

$$
\left(\frac{\partial}{\partial x}\left|f(z)\right|\right)^2+\left(\frac{\partial}{\partial y}\left|f(z)\right|\right)^2=\left|f'(z)\right|^2
$$

#### 共轭调和函数的不可交换性  
若 $f(z)=u+iv$ 解析，则称 $v$ 是 $u$ 的共轭调和函数，但是 $u$ 一般不是 $v$ 的共轭调和函数。

#### 反三角函数和反双曲函数

$$
\operatorname{Arcsin}z=-i\operatorname{Ln}\left(iz+\sqrt{1-z^2}\right)\\
\operatorname{Arccos}z=-i\operatorname{Ln}\left(z+\sqrt{z^2-1}\right)\\
\operatorname{Arctan}z=-\frac{i}{2}\operatorname{Ln}\frac{1+iz}{1-iz}
$$

$$
\operatorname{Arsh}z=\operatorname{Ln}\left(z+\sqrt{z^2+1}\right)\\
\operatorname{Arch}z=\operatorname{Ln}\left(z+\sqrt{z^2-1}\right)\\
\operatorname{Arth}z=\frac{i}{2}\operatorname{Ln}\frac{1+z}{1-z}
$$

#### 光滑曲线

$x'(t)$ 与 $y'(t)$ 均连续，且不同时为 0。

#### 简单曲线

无重点的曲线，即 $\forall t_1, t_2, t_1\neq t_2, z(t_1) \neq z(t_2)$

#### 柯西-黎曼方程的极坐标形式

$$
\frac{\partial u}{\partial r}= \frac{1}{r}\frac{\partial v}{\partial \theta},\\ \ \\
\frac{\partial v}{\partial r}= -\frac{1}{r}\frac{\partial u}{\partial \theta}.
$$