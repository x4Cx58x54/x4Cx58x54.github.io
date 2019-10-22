---
title: 机器学习
---

# 机器学习

>*周志华*  
*2016, 清华大学出版社*  
*2019.9.25 ~  , 长沙*

## 绪论

归纳偏好、奥卡姆剃刀（Occam's razor）和 No Free Lunch 定理证明

## 模型评估与选择

### 经验误差与过拟合

$m$ 个样本中有 $a$ 个样本分类错误，则错误率 $E = a/m$，精度为

$$
\mathrm{accuracy} = 1-E = 1-\frac{a}{m}.
$$

训练误差（经验误差）、泛化误差

### 评估法

划分训练集和测试集的方法

* 留出法 hold-out
* 交叉验证法 cross validation
  * k 折交叉验证 k-fold cross validation
  * 留一法 leave-one-out, LOO
* 自助法 bootstrapping

验证集

### 性能度量

错误率、精度（accuracy）、查准率（precision）、查全率（recall）

P-R 曲线、平衡点（BEP）

F1 值、调和平均、加权调和平均

真正例率、假正例率、ROC、AUC

泛化误差与偏差、方差、噪声