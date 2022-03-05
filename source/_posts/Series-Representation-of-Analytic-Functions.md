---
title: Series Representation of Analytic Functions
date: 2021-12-06 21:16:10
tags: Complex Function
categories: Mathematics 
mathjax: true
---

# 解析函数的级数表示

级数是研究解析函数的另一个重要工具，本章要讨论解析函数的两种级数展开式，并以此为基础进一步研究解析函数。

<!--more-->

## 幂级数

### 收敛

设有复数列$\{z_n=x_n+\mathrm iy_n,n=1,2,\cdots\}$，表达式
$$
\sum\limits_{k=1}^{+\infty}z_k=z_1+z_2+\cdots +z_k+\cdots
$$
称为复数项无穷级数。如果它的部分和数列
$$
S_n=z_1+z_2+\cdots+z_n(n=1,2,\cdots)
$$
有极限$\lim\limits_{n\to+\infty}S_n=S=a+ib$（有限复数），则称级数
$$
\sum\limits_{k=1}^{+\infty}z_k=z_1+z_2+\cdots +z_k+\cdots
$$
是收敛的，$S$称为级数的和，记作
$$
\sum\limits_{k=1}^{+\infty}z_k=S.
$$


### 收敛的充要条件

级数
$$
\sum\limits_{k=1}^{+\infty}z_k=z_1+z_2+\cdots +z_k+\cdots
$$
收敛（于$S$）的充分必要条件是实级数$\sum\limits_{k=1}^{+\infty}a_k$收敛（于$a$）和$\sum\limits_{k=1}^{+\infty}b_k$收敛（于$b$）。

### 绝对收敛

如果级数
$$
\sum\limits_{k=1}^{+\infty}|z_k|=|z_1|+|z_2|+\cdots+|z_k|+\cdots
$$
收敛，则称级数
$$
\sum\limits_{k=1}^{+\infty}z_k=z_1+z_2+\cdots +z_k+\cdots
$$
绝对收敛。

### 阿贝尔定理

1. 如果幂级数
   $$
   \sum\limits_{n=0}^{+\infty}a_n(z-a)^n=a_0+a_1(z-a)+a_2(z-a)^2+\cdots
   $$
   在某点$z_0(z_0\neq a)$收敛，则它在圆$|z-a|<|z_0-a|$内绝对收敛。

2. 如果幂级数
   $$
   \sum\limits_{n=0}^{+\infty}a_n(z-a)^n=a_0+a_1(z-a)+a_2(z-a)^2+\cdots
   $$
   在某点$z_1$发散，则它在圆外域$|z-a|>|z_0-a|$内处处发散。

### 复幂级数的收敛域

设幂级数
$$
\sum\limits_{n=0}^{+\infty}|a_n|x^n
$$
的收敛半径为$R$，则依不同的情况，有：

1. 若$0<R<+\infty$，则级数
   $$
   \sum\limits_{n=0}^{+\infty}a_n(z-a)^n=a_0+a_1(z-a)+a_2(z-a)^2+\cdots
   $$
   在圆$D:|z-a|<R$内绝对收敛；在圆外域$|z-a|>R$内处处发散；

2. 若$R=+\infty$，则级数
   $$
   \sum\limits_{n=0}^{+\infty}a_n(z-a)^n=a_0+a_1(z-a)+a_2(z-a)^2+\cdots
   $$
   在圈平面内收敛；

3. 若$R=0$，则级数
   $$
   \sum\limits_{n=0}^{+\infty}a_n(z-a)^n=a_0+a_1(z-a)+a_2(z-a)^2+\cdots
   $$
   只在复平面内一点$z=a$收敛。

## 解析函数的泰勒展开

### 泰勒级数

设函数$f(z)$在$a$点解析，如果以$a$为中心作一个圆，并让圆的半径不断扩大，直到圆周碰上$f(z)$的奇点为止（如果$f(z)$在全平面上解析，这个圆的半径就是无限大），则在此圆域内部，$f(z)$可以展开成幂级数
$$
f(z)=\sum\limits_{n=0}^{+\infty}a_n(z-a)^n
$$
这里
$$
a_n=\frac{f^{(n)}(a)}{n!}(n=0,1,2,\cdots).
$$

### 泰勒展开与解析

$f(z)$在区域$D$内解析的充分必要条件是$f(z)$在$D$内任一点$a$处可以展开成$z-a$的幂级数。

### m级零点

$f(z)$以$z$为$m$级零点的充要条件是

在$z_0$点附近，有
$$
f(z)=(z-z_0)^mg(z),
$$
这里$g(z)$在$z_0$点解析，且$g(z_0)\neq0$;

或
$$
f(z_0)=f'(z_0)=\cdots=f^{(m-1)}(z_0)=0,
$$
而
$$
f^{(m)}(z_0)\neq 0.
$$

## 解析函数的洛朗展开

### 洛朗级数

设$f(z)$在圆环域$D:r<|z-a|<R$中解析，则$f(z)$一定能在这个圆环中展开成洛朗级数，即
$$
f(z)=\sum\limits_{n=-\infty}^{+\infty}a_n(z-a)^n,
$$
这里
$$
a_n=\frac{1}{2\pi \mathrm i}\int\limits_C\frac{f(\zeta)}{(\zeta-a)^{n+!}}\mathrm d\zeta(n=0,\pm1,\pm2,\cdots),
$$
而$C$是$D$内围绕$a$的任意闭路。

### 孤立奇点

设$f(z)$在点$a$的某个去心邻域$K:0<|z-a|<R$内解析，但在点$a$不解析，则$a$称为$f(z)$的孤立奇点。

如果$f(z)$在$\infty$点的某邻域（即某个圆的外区域）$R<|z|<+\infty$内解析，则$\infty$称为$f(z)$的孤立奇点。

## 孤立奇点的分类

### 可去奇点

设$a$为$f(z)$的孤立奇点，那么$a$是$f(z)$的可去奇点的充分必要条件是：存在某个正数$\rho$，使得$f(z)$在环域$0<|z-a|<\rho$内有界。

### m级极点

设$a$为$f(z)$的孤立奇点，那么$a$是$f(z)$的$m$级极点充分必要条件是：

$f(z)$在某环域内可表示为
$$
f(z)=\frac{\varphi(z)}{(z-a)^m},
$$
这里，$\varphi(z)$在$a$点解析，且$\varphi(a)\neq0$；

或$a$是函数$g(z)=\frac{1}{f(z)}$的$m$级零点。

### 本性奇点

$f(z)$以$a$为本性奇点的充分必要条件是：不存在有限或无限的极限$\lim\limits_{z\to a}f(z)$。

