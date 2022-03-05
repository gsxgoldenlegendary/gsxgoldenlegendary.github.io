---
title: Stationary Process
date: 2021-11-23 15:02:49
tags: Stochastic Process
categories: Mathematics 
mathjax: true
---

# 平稳过程

平稳过程是统计特性不随时间的推移而变化的随机过程。

<!--more-->

## 定义和例子

### 严平稳过程

设$X=\{X(t),t\in T\}$为一随机过程，若对任意正整数$k$及$T$中任意$k$个时刻$t_1<t_2<\cdots<t_k$，及$T$中的$h$，有
$$
\{X(t_1),\cdots,X(t_k)\}\mathop{=}\limits^d\{X(t_1+h),\cdots,X(t_k+h)\},
$$
则随机过程$X$称为严平稳过程。这里“d”表示等式两边$k$维随机向量的分布相同。

### 宽平稳过程

设$X=\{X(t),t\in T\}$为一实值随机过程，如果对$\forall t\in T,EX^2(t)<\infty,EX(t)=m$以及协方差函数$E(X(t)-m)(X(s)-m)$仅与$t-s$有关，则称$X$为宽平稳随机过程。

### Gauss过程

设$G=\{G(t),-\infty<t<\infty\}$为一随机过程，如果对任一正整数$k$以及$k$个时刻$t_1\leqslant t_2\leqslant\cdots\leqslant t_k$，$(G(t_1),G(t_2),\cdots,G(t_k))$的联合分布为$k$维正态分布，则称$G$为Gauss过程。

### 周期平稳过程

设设$X=\{X(t),t\in T\}$为平稳过程，如果存在正整数$\kappa$使$X(t+\kappa)=X(t)$，则$X$称为周期平稳过程，$\kappa$为过程的周期。如果$X$是周期平稳过程，则其协方差函数也是周期函数，且与过程有相同的周期。

## 遍历性定理

### 均值遍历性定理

1. 设$X=\{X_n,0=0,\pm1,\cdots\}$为平稳序列，其协方差函数为$R(\tau)$，则$X$有遍历性的充分必要条件是

$$
\lim\limits_{N\to\infty}\frac 1 N \sum\limits_{\tau=0}^{N-1}R(\tau)=0.
$$

2. 若$X=\{X(t),-\infty<t<\infty\}$为平稳过程，则$X$有遍历性的充分必要条件是

$$
\lim\limits_{T\to\infty}\frac 1 T\int_0^{2T}(1-\frac\tau{2T})R(\tau)\mathrm d\tau=0.
$$

### 平稳过程均值遍历性定理的充分条件

1. 若$\int_{-\infty}^\infty|R(\tau)|\mathrm d\tau<\infty$，则均值遍历性定理成立。
2. 对平稳序列而言，若$R(\tau)\to0(\tau\to\infty)$，则均值遍历性定理成立。

## 平稳过程的协方差函数和功率谱密度

### Wiener-Khintchine公式

假定$EX(t)=0$，且$\int|R(\tau)|d\tau<\infty$，则
$$
s(w)=\int R(\tau)e^{-\mathrm j w\tau}\mathrm d\tau,
$$

$$
R(\tau)=\frac 1{2\pi}\int S(w)e^{\mathrm jwr}\mathrm dw.
$$

