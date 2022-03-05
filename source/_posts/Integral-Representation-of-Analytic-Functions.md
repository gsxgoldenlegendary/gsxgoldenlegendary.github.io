---
title: Integral Representation of Analytic Functions
date: 2021-12-06 19:59:23
tags:  Complex Function
categories: Mathematics 
mathjax: true
---

# 解析函数的积分表示

复积分是研究解析函数的一个重要工具，解析函数的许多重要性质都是通过它的积分表示得到的，这是复变函数论在方法上的一个特点。

<!--more-->

## 复变函数的积分

### 复变函数的积分

设$C$是平面上的一条有向曲线，其起点是$z_0$，终点是$Z$，$f(z)$是定义在$C$上的单值函数。任意用一列分点
$$
z_k=x_k+y_k(k=0,1,\cdots,n,z_n=Z)
$$
把曲线$C$分成$n$个小段，在每个小段$\overset{\LARGE\frown}{z_{k-1} z_k}$上任取点$\zeta_k$，作和
$$
\sum\limits_{k=1}^nf(\zeta_k)\Delta z_k(\Delta z_k=z_k-z_{k-1}).
$$
记$\lambda=\max\limits_k|\Delta z_k|$，如果当$\lambda\to0$时，上述和式的极限存在，而且其值与弧段的分法和各$\zeta_k$的取法无关，就称这个极限为$f(z)$沿曲线$C$自$z_0$到$Z$的积分，记作
$$
\int\limits_Cf(z)\mathrm dz.
$$


### 复变函数积分与第二型曲线积分

设$f(z)=u(x,y)+\mathrm iv(x,y)$在曲线$C$上连续，则复积分$\int\limits_Cf(z)\mathrm dz$存在，而且
$$
\int\limits_Cf(z)\mathrm dz=\int\limits_Cu(x,y)\mathrm dx-v(x,y)\mathrm dy\newline+\mathrm i\int\limits_Cv(x,y)\mathrm dx+u(x,y)\mathrm dy
$$

## 柯西积分定理

### 柯西积分定理

设$D$是由闭路$C$所围成的单连通区域，$f(z)$在闭区域$\overline D=C+D$上解析，则
$$
\int\limits_Cf(z)\mathrm dz=0.
$$
这里，所谓$f(z)$在闭域$D$上解析，是指存在区域$G$，使得$\overline D\subset G$，且$f(z)$在$G$内解析。

### 多连通区域的柯西积分定理

设$f(z)$在复闭路$C=C_0+C_1^-+C_2^-+\cdots+C_n^-$及其所围成的多连通区域内解析，则
$$
\int\limits_{C_0}f(z)\mathrm dz=\int\limits_{C_1}f(z)\mathrm dz+\int\limits_{C_2}f(z)\mathrm dz+\cdots+\int\limits_{C_n}f(z)\mathrm dz
$$
或
$$
\int\limits_Cf(z)\mathrm dz=0.
$$

## 柯西积分公式

### 柯西积分公式

设函数$f(z)$在闭路（或复闭路）$C$及其所围区域$D$内解析，则对$D$内任一点$z$，有
$$
f(z)=\frac{1}{2\pi \mathrm i}\int\limits_C\frac{f(\zeta)}{\zeta-z}\mathrm d\zeta.
$$


### 柯西积分公式

设函数$f(z)$在闭路（或复闭路）$C$及其所围区域$D$内解析，则对$D$内任一点$z$，$f(z)$有任意阶导数，且
$$
f^{(n)}(z)=\frac{n!}{2\pi \i}\int\limits_C\frac{f(\zeta)}{(\zeta-z)^{n+!}}\mathrm d\zeta.
$$

## 原函数

### 原函数

如果在区域$D$内有$F'(z)=f(z)$，则$F(z)$称为$f(z)在区域$D内的一个原函数。

### 原函数与变上限积分

设$f(z)$在单连通区域$D$内连续，且对$D$内任意闭路$C$，有$\int\limits_Cf(z)=\mathrm dz=0$，那么，由变上限积分所确定的函数
$$
F(z)=\int_{z_0}^zf(z)\mathrm dz
$$
（$z_0$是$D$内一定点）是$D$内的解析函数，而且
$$
F'(z)=f(z)(z\in D).
$$

### 莫累拉定理

设$f(z)$在单连通区域$D$内连续，且对$D$内任意闭路$C$，有$\int\limits_Cf(z)=\mathrm dz=0$，那么$f(z)$是$D$内的解析函数。

## 解析函数与调和函数的关系

### 调和函数

如果实二元函数$u(x,y)$在区域$D$内有二阶连续偏导数，且在$D$内满足拉普拉斯方程
$$
\frac{\partial^2 u}{\partial x^2}+\frac{\partial^2 u}{\partial y^2}=0,
$$
则称$u(x,y)$是域$D$内的调和函数。

### 由解析推调和

设$f(z)=u(x,y)+iv(x,y)$在域$D$内解析，那么它的实部$u$及虚部$v$都是$D$的调和函数。

### 解析函数的几何性质

设$f(z)=u+iv$是一解析函数，且$f'(z)\neq 0$，那么等值曲线族
$$
u(x,y)=K_1
$$
与
$$
v(x,y)=K_2
$$
在其公共点上永远是相互正交的，这里，$K1$及$K_2$为常数。

### 由调和找解析

设$u(x,y)$是单连通区域$D$内的调和函数，则由线积分所确定的函数
$$
v(x,y)=\int_{(x_0,y_0)}^{(x,y)}-\frac{\partial u}{\partial y}\mathrm dx+\frac{\partial u}{\partial x}\mathrm dy+C
$$
使得$f(z)=u(x,y)+iv(x,y)$在$D$内解析。其中，$(x,y)$是$D$内任一点，$(x_0,y_0)$是$D$内一定点，$C$是实常数。
