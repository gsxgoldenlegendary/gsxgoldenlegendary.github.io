---
title: Residue and Its Applications
date: 2021-12-07 13:15:11
tags: Complex Function
categories: Mathematics 
mathjax: true
---

# 留数及其应用

留数是复变函数中的一个重要概念，它有着广泛的应用。本章先讲述留数的一般理论，然后介绍它的一些应用，特别是在计算某些类型的定积分中的应用。

<!--more-->

## 留数定理

### 留数定理

如果函数$f(z)$在闭路$C$上解析，在$C$的内部除去$n$个孤立奇点$a_1,a_2,\cdots,a_n$外也解析，则
$$
\int\limits_Cf(z)\mathrm dz=2\pi\mathrm i\sum\limits_{k=1}^nRes[f(z),a_k].
$$

### 极点的留数

设$a$是$f(z)$的$m$级极点，则
$$
Res[f(z),a]=\frac 1{(m-1)!}\lim\limits_{z\to a}\frac{\mathrm d^{m-1}}{\mathrm dz^{m-1}}[(z-a)^mf(z)].
$$

## 定积分的计算

### 引理1

如果当$R$充分大时，$f(z)$在圆弧$C_R:z=Re^{i\theta}(\alpha\leqslant\theta\leqslant\beta)$上连续，且
$$
\lim\limits_{z\to\infty}zf(z)=0,
$$
则
$$
\lim\limits_{R\to+\infty}\int\limits_{C_R}f(z)\mathrm dz=0.
$$

### 引理2

如果当$\rho$充分小时，$f(z)$在圆弧
$$
C_\rho:z=a+\rho e^{\mathrm i\theta}(\alpha\leqslant\theta\leqslant\beta)
$$
上连续，且
$$
\lim\limits_{z\to a}(z-a)f(z)=k,
$$
则
$$
\lim\limits_{\rho\to0}\int\limits_{C_\rho}f(z)\mathrm dz=\mathrm  i(\beta-\alpha)k.
$$

### 若尔当引理

如果$R$充分大时，$g(z)$在圆弧
$$
C_R:|z|=R,\Im z>-a(a>0)
$$
上连续，且
$$
\lim\limits_{z\to\infty}g(z)=0,
$$
则对任何正数$\lambda$，都有
$$
\lim\limits_{R\to+\infty}\int\limits_{C_R}g(z)e^{\mathrm i\lambda z}\mathrm dz=0.
$$
