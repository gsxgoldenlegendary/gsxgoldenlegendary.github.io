---
title: Introduction of Stochastic Process
date: 2021-10-26 18:58:06
tags: Stochastic Process
categories: Mathematics 
mathjax: true
---

# 引论

一般来说，把一组随机变量定义为随机过程。在研究随机过程时人们透过表面的偶然性描述出必然的内在规律并以概率的形式来描述这些规律，从偶然中悟出必然正是这一学科的魅力所在。

<!--more-->

## 引言

### 随机过程

随机过程就是一族随机变量$\{X(t),t\in T\}$，其中$t$为参数，它属于某个指标集$T$，$T$称为参数集。

### 严格平稳 

如果随机过程$X(t)$对任意的$t_1,\cdots,t_n\in T$和任何$h$有$$(X(t_1+h),\cdots,X(t_n+h)) \mathop{=}\limits^d(X(t_1),\cdots,X(t_n))$$，则称为严格平稳的。

### 宽平稳

如果随机过程的所有二阶矩存在并有$EX(t)=m$及协方差函数$R_X(t,s)$只与时间差$t-s$有关，则称为宽平稳的或二阶矩平稳的。

### 独立增量过程

如果对任意$t_1<t_2<\cdots<t_n,t_1,\cdots,t_n\in T$，随机变量是相互独立的，则$X(t)$称为独立增量过程。如果进一步有对任意的$t1,t2$，$$X(t_1+h)-X(t_1)\mathop{=}\limits^dX(t_2+h)-X(t_2)$$，则过程称为有平稳独立增量的过程。

## 条件期望与矩母函数

### 条件期望的重要性质

若$X$与$Y$独立，则$E(X|Y=y)=EX$。

条件期望有所谓的平滑性：$EX=\int E(X|Y=y)dF_Y(y)=E[E(X|Y)]$。

对随机变量$X,Y$的函数$\phi(X,Y)$，恒有$$E[\phi(X,Y)|Y=y]=E[\phi(X,y)|Y=y]$$。

### 矩母函数

随机变量$X$的矩母函数定义为随机变量$e^{tX}$的期望，记作$g(t)$，即$g(t)=E(e^{tX})=\int e^{tX}dF(x)$。

### 概率生成函数

若$X$为离散随机变量，则期望$E(s^X)$为其概率生成函数。记作$\phi_X(s)$。特别地，若$P(X=k)=p_k,k=0,1,2,\cdots$，则$\phi_X(s)=\sum\limits_{k=0}\limits^\infty p_ks^k$。

## 收敛性

### 依概率收敛和几乎必然收敛

设$\{X_n,n\geqslant1\}$是一列随机变量，若存在随机变量$X$，使对$\forall \varepsilon>0$，有$\lim\limits_{n\to\infty}P(|X_n-X|\geqslant\varepsilon)=0$，则称随机变量序列$\{X_n,n\geqslant1\}$依概率收敛于$X$，记为$X_n\mathop\to\limits^p X$。

如果事件$\{\omega:\lim\limits_{n\to\infty}(X_n(\omega)-X(\omega))=0\}$的概率为$1$，即$P(\lim\limits_{n\to\infty}(X_n-X)=0)=1$，则称随机变量序列$\{X_n,n\geqslant1\}$几乎必然收敛于$X$，记为$X_n\to X,a.s.$，也称随机变量序列以概率$1$收敛于$X$。

### 均方收敛

设随机变量$X$和$X_n,n\geqslant1$，都有有限的二阶矩，如果$\lim\limits_{n\to\infty}E(X_n-X)^2=0$，则称$X_n$军方收敛于$X$，记为$X_n\mathop\to\limits^{L_2}X$。

## 难题集萃

### 期望不等式

$X,Y$为随机变量，$EX,EY,Eg(Y)$存在，证明：$E(Y-E(Y|X))^2\leqslant E(Y-g(X))^2$。

解：
$$
E((Y-E(Y|X))^2-(Y-g(X))^2)
\\=E((2Y-E(Y|X)-g(X))(g(X)-E(Y|X)))
\\=E(E(((2Y-E(Y|X)-g(X))(g(X)-E(Y|X)))|X))
\\=E(-(g(X))^2+2g(XE(Y|X))-(E(Y|X))^2)
\\=-E(g(X)-E(Y|X))^2
\\  \leqslant0.
$$
