---
title: 离散数学
---

# 离散数学

## 集合论

$
\Sigma^* = \Sigma^0 \cup \Sigma^1 \cup \Sigma^2 \cup \Sigma^3 \cdots
$

$
\Sigma^+ = \Sigma^* - \Sigma^0
$

## 二元关系

传递关系的交集仍传递，但对其他运算无此性质.

$
R_2\subseteq R_3 \Rightarrow R_1R_2\subseteq R_1R_3 \land R_2R_4\subseteq R_3R_4 
$

$
R_1(R_2\cup R_3)=R_1R_2\cup R_1R_3, \quad (R_2\cup R_3)R_4=R_2R_4\cup R_3R_4
$

$
R_1(R_2\cap R_3)\subseteq R_1R_2\cap R_1R_3, \quad (R_2\cap R_3)R_4\subseteq R_2R_4\cap R_3R_4
$

$R^{-1}$ 保持其原自反、反自反、对称、反对称、传递、反传递性质.

$R_1\circ R_2$ 仅能保持其自反性质.

$R$ 传递 $\Rightarrow R^2\subseteq R$

$R$ 反传递 $\Rightarrow R^2\cap R=\varnothing$

相容关系：自反、对称. $sr(R)$

等价关系：自反、对称、传递. $tsr(R)$

$
st(R)\subseteq ts(R)
$

构造反例证明“传递关系的对称闭包不传递”：简单的传递关系 1 > 2 > 3.

## 图论

$(p, q)$ 图：顶点数为 $p$，边数为 $q$ 的无向图. 

$k$ 度正则图：各顶点次数均为 $k$.

$K_p$：$p$ 阶完全图.

$K_{m,n}$：完全二部图.

生成子图：去掉某些边.

导出子图：去掉某些点及其相关边.