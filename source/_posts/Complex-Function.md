---
title: Complex Function
date: 2021-12-06 13:02:46
tags: Complex Function
categories: Mathematics 
mathjax: true
---

# 复变数函数

本章引入复变数函数、极限、连续和导数的概念，然后讨论复变函数论的主要研究对象——解析函数，这类函数在理论和实际问题中都有着广泛的应用，接着介绍一些常见的复初等函数及它们的基本性质。

<!--more-->

## 复变数函数

### 复变数函数

设$E$是复平面上的一个点集，若对于$E$中的每一个点$z$，按一定规律有一个复数$w$与之相对应，则称在$E$上定义了一个复单值函数，记作$w=f(z)(z\in E)$；如果对于自变量$z$的一个值，按规律与之对应的$w$不止一个，则称$w=f(z)$是多值函数。

### 复变函数与变换

设$w=f(z)$是集合$E$上的单值函数，如果对于$E$中任意两个不同点$z_1$及$z_2$，它们在（函数值）集合$e'$中对应的点$w_1=f(z_1)及$$w_2=f(z_2)$也不同，则称$w=f(z)$是集$E$中的一个一一映照（或双方单值映照）。或者说，$w=f(z)$双方单值地把集$E$映成集$E'$。

## 函数的极限和连续性

### 复数列的极限

设函数$w=f(z)$在点$z_0$的某个去心邻域$0<|z-z_0|<\rho$内有定义，而且实极限
$$
\lim\limits_{z\to z_0}|f(z)-w_0|=0,
$$
就称当$z$趋于$z_0$时$f(z)$的极限为$w_0$，记作
$$
\lim\limits_{z\to z_0}f(z)=w_0
$$

### 复函数的连续

如果等式
$$
\lim\limits_{z\to z_0}f(z)=f(z_0)
$$
成立，就称函数$f(z)$在点$z_0$连续，如果$f(z)$在区域$D$中的每点都连续，就称$f(z)$在区域$D$中连续。

### 复函数的连续的充要条件

函数$f(z)=u(x,y)+\mathrm iv(x,y)$在点$z_0=x_0+iy_0$处连续的充要条件是$u(x,y)$和$v(x,y)$作为二元函数在$(x_0,y_0)$处连续。

### 复函数的极限

设$w=f(z)$在点$z$的某个邻域$U$内有定义，$z+\Delta z\in U$，如果极限
$$
\lim\limits_{\Delta z\to 0}\frac{f(z+\Delta z)-f(z)}{\Delta z}
$$
存在，就称函数$f(z)$在点$z$可微，而且这个极限称为$f(z)$在点$z$的导数或微商，记为$f'(z),\frac{\mathrm df}{\mathrm dz}$或$\frac{\mathrm d w}{\mathrm dz}$。即
$$
f'(z)=\lim\limits_{\Delta z\to 0}\frac{f(z+\Delta z)-f(z)}{\Delta z}.
$$


### 解析与奇点

如果$f(z)$在区域$D$内的每一点可微，则称$f(z)$在$D$内解析，或者说$f(z)$是$D$内的解析函数；如果$f(z)$在点$z_0$的某个邻域内可微，则称$f(z)$在点$z_0$解析；如果$f(z)$在点$z_0$不解析，则$z_0$称为$f(z)$的奇点。

## 柯西——黎曼方程

### 复函数在某点可微的充要条件

函数$f(z)=u(x,y)+\mathrm iv(x,y)$在点$z=x+\mathrm iy$可微的充分必要条件是：

1. 二元函数$u(x,y),v(x,y)$在点$(x,y)$可微；
2. $u(x,y)$及$v(x,y)$在点$(x,y)$满足柯西——黎曼方程（简称C-R方程）

$$
\frac{\partial u}{\partial x}=\frac{\partial v}{\partial y},\newline \frac{\partial u}{\partial y}=-\frac{\partial v}{\partial x}.
$$

### 复函数在区间上可微的充要条件

函数$f(z)=u(x,y)+\mathrm iv(x,y)$在区间$D$内可微（即在D内解析）的充分必要条件是：

1. 二元函数$u(x,y),v(x,y)$在$D$内可微；
2. $u(x,y)$及$v(x,y)$在$D$内处处满足C-R方程。

