---
title: Random Variables and Probability Distributions
date: 2021-10-28 10:42:48
tags: Probability Theory
categories: Mathematics 
mathjax: true
---

简单地说，随机变量是指随机事件的数量表现。

<!--more-->

# 一维随机变量

## 随机变量的概率函数

设$X$为离散型随机变量，其全部可能值为$\{a_1,a_2,\cdots\}$，则
$$
p_i=P(X=a_i)	(i=1,2,\cdots)
$$
称为的概率函数。

## 随机变量的分布函数

设$X$为一随机变量，则函数
$$
P(X\leqslant x)=F(X)(-\infty<x<\infty)
$$
称为的分布函数。

## 随机变量的概率密度函数

设连续型随机变量$X$的概率分布函数$F(x)$，则$F(X)$的导数$f(x)=F'(x)$称为$X$的概率密度函数。

## Poisson 分布

若随机变量$X$的可能取值为$0,1,2,\cdots$，且概率分布为
$$
P(X+i)=e^{-\lambda}\frac{\lambda^i}{i!}
$$
，则称服从Poisson分布，常记为。此处，是某一常数。

## 正态分布

如果一个随机变量$X$具有概率密度函数
$$
f(x)=\frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{(x-\mu)^2}{2\sigma^2}}(-\infty<x<\infty)
$$
，则称$X$为正态随机变量，并记为$X\sim N(\mu,\sigma^2)$。

## 指数分布

若随机变量$X$有概率密度函数
$$
f(x)=\lambda e^{-\lambda x},当x>0时;0,当x\leqslant0时
$$
，则称$X$服从指数分布。其中，$\lambda>0$为参数。

## 均匀分布

设随机变量$X$有概率密度函数
$$
f(x)=\frac{1}{b-a},当a\leqslant x\leqslant b时;0,其他
$$
，则称$X$服从区间$[a,b]$上的均匀分布，并常记为$X\sim R(a,b)$。这里，$a,b$都是常数，$-\infty<a<b<\infty$。

# 多维随机变量（随机向量）

## 随机向量的概率函数

以$\{a_{i1},a_{i2}.\cdots\}$记$X_i$的全部可能值$(i=1,2,\cdots)$，则事件
$$
\{X_1=a_{1j_1},X_2=a_{2j_2},\cdots,X_n=a_{nj_n}\}
$$
的概率
$$
p(j_1,j_2,\cdots,j_n)=P(X_1=a_{1j_1},X_2=a_{2j_2},\cdots,X_n=a_{nj_n})(j_1=1,2,\cdots;j_2=1,2,\cdots;\cdots;j_n=1,2,\cdots)
$$
称为随机向量的概率函数或概率分布，概率函数应满足条件
$$
p(j_1,j_2,\cdots,j_n)\geqslant0,\sum\limits_{j_n}\cdots\sum\limits_{j_2}\sum\limits_{j_1}p(j_1,j_2,\cdots,j_n)=1
$$

## 随机向量的概率密度函数

若$f(x_1,\cdots,x_n)$是定义在$\mathbb{R}^n$的非负函数，使对$\mathbb{R}^n$中的任何集合$A$，有
$$
P(X\in A)=\mathop{\int\cdots\int}\limits_Af(x_1,\cdots,x_n)\mathrm{d}x_1\cdots \mathrm{d}x_n
$$
，则称$f$是$X$的（概率）密度函数。

## 随机向量的边缘分布

设$X=(X_1,\cdots,X_n)$为一个$n$维的随机变量，$X$有一定的分布$F$，这是一个$n$维分布，因为$X$的每个分量$X_i$都是一维随机变量，故它们都有各自的分布$F_i(i=1,\cdots,n)$这些都是一维分布，称为随机向量$X$或分布$F$的“边缘分布”。

## 多项分布

设$A_1,A_2,\cdots,A_n$是某一试验之下的完备事件群。分别以$p_1,p_2,\cdots,p_n$记事件$A_1,A_2,\cdots,A_n$的概率，则$p_i\geqslant0,p_1+p_2+\cdots+p_n=1$。现将试验独立地重复$N$次，而以$X_i$记在这$N$次试验中事件$A_i$出现的次数$X=(X_1,\cdots,X_n)$为一个$n$维随机向量。$X$的概率分布就叫多项分布，有时记为$M(N;p_1,\cdots,p_n)$。
$$
P(X_1=k_1,X_2=k_2,\cdots,X_n=k_n)=\frac{N!}{k_1!k_2!\cdots k_n!}p_1^{k_1}p_2^{k_2}\cdots p_n^{k_n}(k_i为非负整数,k_1+k_2+\cdots+k_n=N)
$$

## 二维正态分布 

其概率密度函数有形式
$$
f(x_1,x_2)=\frac{1}{2\pi\sigma_1\sigma_2\sqrt{1-\rho^2}}e^{-\frac{1}{2(1-\rho^2)}(\frac{(x_1-a)^2}{\sigma_1^2}-\frac{2\rho(x_1-a)(x_2-b)}{\sigma_1\sigma_2}+\frac{(x_2-b)^2}{\sigma_2^2})}
$$

# 条件概率分布与随机变量的独立性

## 离散型随机变量的条件概率分布

设$(X_1,X_2)$为一个二维离散型随机向量，$X_1$的全部可能值为$a_1,a_2,\cdots$；的全部可能值为$b_1,b_2,\cdots$；而$(X_1,X_2)$的联合概率分布为
$$
p_{ij}=P(X_1=a_i,X_2=b_j)(i,j=1,2,\cdots).
$$
现在考虑$X_1$在给定的条件$X_2=b$下的条件分布，那无非是要找条件概率$P(X_1=a|X_2=b_j)$。依条件概率的定义，有
$$
P(X_1=a|X_2=b_j)=\frac{P(X_1=a_i,X_2=b_j)}{P(X_2=b_j)}=\frac{p_{ij}}{\sum\limits_kp_{kj}}.
$$

## 连续型随机变量的条件概率分布

设二维随机变量$X=(X_1,X_2)$在概率密度函数$f(x_1,x_2)$，我们先来考虑在限定$a\leqslant x_2\leqslant b$的条件下$X_1$的条件分布，有
$$
P(X_1\leqslant x_1|a\leqslant x_2\leqslant b)=\frac{P(X_1\leqslant x_1,a\leqslant x_2\leqslant b)}{P(a\leqslant x_2\leqslant b)}
$$

$$
=\frac{\int_{-\infty}^{x_1}\mathrm{d}t_1\int_a^bf(t_1,t_2)\mathrm{d}t_2}{\int_a^bf_2(t_2)\mathrm{d}t_2}
$$

对$x_1$求导数，得到条件密度函数为
$$
f_1(x_1|a\leqslant x_2\leqslant b)=\frac{\int_a^bf(x_1,t_2)\mathrm{d}t_2}{\int_a^bf_2(t_2)\mathrm{d}t_2}
$$

## 离散型随机变量的独立性

设$X_1,\cdots,X_n$都是离散型随机变量，若对任何常数$a_1,\cdots,a_n$，都有
$$
P(X_1=a_1,\cdots,X_n=a_n)=P(X_1=a_1)\cdots P(X_n=a_n),
$$
则称$X_1,\cdots,X_n$相互独立。

## 连续型随机变量的独立性

设$n$维随机变量$(X_1,\cdots ,X_n)$的联合密度函数为$f(x_1,\cdots,x_n)$，而$X_i$的边缘密度函数为$f_i(x_i)(i=1,\cdots,n)$。如果
$$
f(x_1,\cdots,x_n)=f(x_1)\cdots f(x_n),
$$
则称随机变量$X_1,\cdots,X_n$相互独立，或简称独立。

## 事件的独立性

如果连续变量$X_1,\cdots ,X_n$独立，则对任何$a_i<b_i(i=1,\cdots,n)$，由$A_i=\{a_i\leqslant X_i\leqslant b_i\}(i=1,\cdots n)$定义的$n$个事件$A_1,\cdots,A_n$也独立。反之，若对任何$a_i<b_i(i=1,\cdots,n)$，事件$A_1,\cdots,A_n$独立，则变量$X_1,\cdots,X_n$也独立。

## 随机向量分量的独立性

若连续型随机向量$(X_1,\cdots,X_n)$的概率密度函数可表为$n$个函数$g_1(x),\cdots,g_n(x)$之积，其中$g_i(x)$只依赖于$x_i$，即
$$
f(x_1,\cdots,x_n)=g_1(x_1)\cdots g_n(x_n)
$$
则$X_1,\cdots ,X_n$相互独立，且$X_i$的边缘密度函数$f_i(x_i)$与$g_i(x_i)$只相差一个常数因子。

## 随机变量函数的独立性

若$X_1,\cdots,X_n$相互独立，而
$$
Y_1=g_1(X_1,\cdots,X_m),Y_2=g_2(X_{m+1},\cdots,X_n),
$$
则$Y_i$和$Y_2$独立。

# 随机变量的函数的概率分布

## 连续型随机变量的函数的概率分布

设$X$有密度函数$f(x)$，设$Y=g(x)$，$g$严格单调，则$Y$的分布函数
$$
P(Y\leqslant y)=P(g(X)\leqslant Y)=P(X\leqslant g^{-1}(y))=\int_{-\infty}^{h(y)}f(t)\mathrm{d}t,
$$
或
$$
P(Y\leqslant y)=P(g(X)\leqslant Y)=P(X\geqslant g^{-1}(y))=\int^\infty_{h(y)}f(t)\mathrm{d}t,
$$
对$y$求导数，得$Y$的密度函数
$$
l(y)=f(g^{-1}(y))(g^{-1}(x))',
$$
或
$$
l(y)=-f(g^{-1}(y))(g^{-1}(x))',
$$
总有
$$
l(y)=f(g^{-1}(y))|(g^{-1}(x))'|.
$$

## 连续型随机向量的函数的概率分布

设$(X_1,X_2)$的密度函数为$f(x_1,x_2)$，
$$
Y_1=g_1(X_1,X_2),Y_2=g_2(X_1,X_2)
$$
都是$(X_1,X_2)$的函数。假设$g_1,g_2$是一一对应变换，因而有逆变换$h_1,h_2$，再假定$g_1,g_2,h_1,h_2$都有一阶偏导数，则变换的Jacobi行列式为
$$
J(y1,y2)=\frac{\partial h_1}{\partial y_1}\frac{\partial h_2}{\partial y_2}-\frac{\partial h_1}{\partial y_2}\frac{\partial h_2}{\partial y_1}
$$
则$(Y_1,Y_2)$的密度函数为
$$
l(y_1,y_2)=f(h_1(y_1,y_2),h_2(y_1,y_2))|J(y_1,y_2)|.
$$

## 随机变量和的密度函数

设$(X_1,X_2)$的联合密度函数为$f(x_1,x_2)$，则$Y=X_1+X_2$的密度函数为
$$
l(y)=\int_{-\infty}^\infty f_1(x)f_2(y-x)\mathrm{d}x.
$$

## 随机变量商的密度函数

设$(X_1,X_2)$的联合密度函数为$f(x_1,x_2)$，$X_1$只取正值，则$Y=\frac{X_2}{X_1}$的密度函数为
$$
l(y)=\int_0^\infty x_1f(x_1,yx_1)\mathrm{d}x_1.
$$

# 统计三大分布

## 卡方分布

### 定义

若
$$
X_1,\cdots,X_n\ \mathrm{iid.},\sim N(0,1).
$$
则
$$
Y=X_1^2+\cdots,X_n^2
$$
服从自由度为$n$的卡方分布$\chi_n^2$。

### 可加性

如果$X\sim\chi_{n_1}^2,Y\sim\chi_{n_2}^2$，并且$X,Y$相互独立，则
$$
X+Y\sim\chi_{n_1+n_2}^2.
$$

### 期望与方差

若$X\sim\chi_n^2$，则$EX=n,D(X)=2n$。

## t分布

### 定义

设随机变量$X$与$Y$相互独立，且$X\sim N(0,1)，Y\sim \chi_n^2$，则称统计量$T=\frac X {\sqrt\frac Y n}$服从自由度为$n$的$t$分布，记作$T\sim t_n$。

## F分布

### 定义

若$U\sim \chi_{n_1}^2,V\sim \chi_{n_2}^2$，且$u$与$V$相互独立，则称统计量$\frac {\frac U {n_1}} {\frac V {n_2}}$服从自由度为$(n_1,n_2)$的$F$分布，记为$F_{n_1,n_2}$。

### 性质

若$F\sim F_{n_1,n_2}$，则$\frac 1 F\sim F_{n_2,n_1}$。

若$t\sim t_n$，则$t^2\sim F_{1,n}$。

