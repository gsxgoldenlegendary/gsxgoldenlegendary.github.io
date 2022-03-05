---
title: Figure Characteristic of Random Variable
date: 2021-11-11 10:08:10
tags: Probability Theory
categories: Mathematics 
mathjax: true
---

# 随机变量的数字特征

数字特征是指能够刻画随机变量某些方面的性质特征的量称为随机变量的数字特征。 比较常用的数字特征有数学期望，方差，协方差和相关系数等。

<!--more-->

## 数学期望（均值）与中位数

### 取有限个值的离散型随机变量的数学期望

设随机变量$X$只取有限个可能值$a_1,a_2,\cdots,a_m$，其概率分布为
$$
P(X=a_i)=p_i,i=1,\cdots,m,
$$
则$X$的数学期望，记为$E(X)$，或EX，定义为
$$
E(X)=a_1p_1+a_2p_2+\cdots+a_mp_m.
$$

### 取无限个值的离散型随机变量的数学期望

设随机变量$X$取无限个可能值$a_1,a_2,\cdots$，其概率分布为
$$
P(X=a_i)=p_i,i=1,2,\cdots,
$$
如果
$$
\sum\limits_{i=1}^\infty|a_i|p_i<\infty,
$$
则称
$$
E(X)=\sum\limits_{i=1}^\infty a_ip_i
$$
为$X$的数学期望。

### 连续型随机变量的数学期望

设$X$的概率密度函数$f(x)$，如果
$$
\int_{-\infty}^\infty|x|f(x)\mathbf{d}x<\infty,
$$
则称
$$
E(X)=\int_{-\infty}^\infty xf(x)\mathbf{d}x
$$
为$X$的数学期望。

### 随机变量和的数学期望

若干个随机变量之和的期望等于各随机变量的期望之和，即
$$
E(X_1+X_2+\cdots+X_n)=E(X_1)+E(X_2)+\cdots+E(X_n).
$$

### 随机变量积的数学期望

若干个随机变量之积的期望等于各随机变量的期望之积，即
$$
E(X_1X_2\cdots X_n)=E(X_1)E(X_2)\cdots E(X_n).
$$

### 随机变量函数的数学期望

设随机变量$X$为离散型，有分布$P(X=a_i)=p_i(i=1,2,\cdots)$；或为连续型，有概率密度函数$f(x)$，则
$$
E(g(X))=\sum\limits_ig(a_i)p_i(当\sum\limits_i|g(a_i)|p_i<\infty 时),
$$
或
$$
E(g(X))=\int_{-\infty}^\infty g(x)f(x)\mathrm{d}x(当\int_{-\infty}^\infty |g(x)|f(x)\mathrm{d}x时).
$$

### 条件数学期望（条件均值）

在给定了某些其他随机变量$X,Z,\cdots$的值$x,z,\cdots$的条件之下$Y$的条件期望，记为$E(Y|X=x,Z=z,\cdots)$。以只有一个变量$X$为例，就是$E(Y|X=x)$。在$X$已明确而不致引起误解的情况下，也可简记为$E(Y|x)$。
$$
E(Y|x)=\int_{-\infty}^\infty yf(y|x)\mathrm{d}y.
$$

### 中位数

设连续型随机变量$X$的分布函数为$F(X)$，则满足条件
$$
P(X\leqslant m)=F(m)=\frac{1}{2}
$$
的数$m$称为$X$或分布$F$的中位数。

## 方差与矩

### 方差和标准差

设$X$为随机变量，分布为$F$，则
$$
\mathrm{Var}(X)=E(X-EX)^2
$$
称为$X$（或分布$F$）的方差，其算数平方根$\sqrt{\mathrm{Var}(X)}$称为$X$（或分布$F$）的标准差。

### 方差的基本性质

1. 常数的方差为$0$。
2. 若$c$为常数，则$\mathrm{Var}(X+c)=\mathrm{Var}(X)$。
3. 若$c$为常数，则$\mathrm{Var}(cX)=c^2\mathrm{Var}(X)$。

### 随机变量和的方差

独立随机变量之和的方差等于各变量的方差之和，即
$$
\mathrm{Var}(X_1+\cdots+X_n)=\mathrm{Var(X_1)}+\cdots+\mathrm{Var}(X_n).
$$

### 矩

设$X$为随机变量，$c$为常数，$k$为正整数，则量$E((X-c)^k)$称为$X$关于$c$点的$k$阶矩。

## 协方差与相关系数

### 协方差

称
$$
E((X-E(X))(Y-E(Y)))
$$
为$X,Y$的协方差，并记为$\mathrm{Cov}(X,Y)$。

### 协方差的重要性质

1. 若$X,Y$独立，则$\mathrm{Cov}(X,Y)=0$。
2. $(\mathrm{Cov}(X,Y))^2\leqslant \sigma_1^2\sigma_2^2$，等号当且仅当$X,Y$之间有严格线性关系（即存在常数$a,b$使$Y=a+bX$）时成立。

### 相关系数

称$\frac{\mathrm{Cov}(X,Y)}{\sigma_1\sigma_2}$为$X,Y$的相关系数，并记为$\mathrm{Corr}(X,Y)$。

### 相关系数的重要性质

1. 若$X,Y$独立，则$\mathrm{Corr}(X,Y)=0$。
2. $(-1\leqslant\mathrm{Corr}(X,Y)\leqslant 1$，等号当且仅当$X,Y$之间有严格线性关系时达到。

## 大数定理和中心极限定理

### 大数定理

设$X_1,X_2,\cdots,X_n,\cdots$是独立同分布的随机变量，记它们的公共均值为$a$，有设它们的方差存在并记为$\sigma^2$，则对任意给定的$\varepsilon>0$，有
$$
\lim\limits_{n\to\infty}P(|\overline{X_n}-a|\geqslant\varepsilon)=0.
$$

### 马尔科夫不等式

若$Y$为只取非负值的随机变量，则对任给常数$\varepsilon>0$，有
$$
P(Y\geqslant\varepsilon)\leqslant\frac{E(Y)}{\varepsilon}.
$$

### 契比雪夫不等式

若$\mathrm{Var}(Y)$存在，则
$$
P(|Y-EY|\geqslant\varepsilon)\leqslant\frac{\mathrm{Var}(Y)}{\varepsilon^2}.
$$

### 林德伯格定理

设$X_1,X_2,\cdots,X_n,\cdots$为独立同分布的随机变量，
$$
E(X_i)=a,\mathrm{Var}(X_i)=\sigma^2(0<\sigma^2<\infty),
$$
则对任何实数$x$，有
$$
\lim\limits_{n\to\infty}P(\frac{1}{\sqrt{n}\sigma}(X_1+\cdots+X_n-na)\leqslant x)=\Phi(x).
$$
这里，$\Phi(x)$是标准正态分布$N(0,1)$的分布函数，即
$$
\Phi(x)=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty}e^{-\frac{t^2}{2}}\mathrm{d}t.
$$

### 历史上最早的中心极限定理

设$X_1,X_2,\cdots,X_n,\cdots$独立同分布，$X_i$的分布是
$$
P(X_i=1)=p,P(X_i=0)=1-p(0<p<1).
$$
则对任何实数$x$，有
$$
\lim\limits_{n\to\infty}P(\frac{1}{\sqrt{np(1-p)}}(X_1+\cdots+X_n-np)\leqslant x)=\Phi(x).
$$
这里，$\Phi(x)$是标准正态分布$N(0,1)$的分布函数，即
$$
\Phi(x)=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty}e^{-\frac{t^2}{2}}\mathrm{d}t.
$$

