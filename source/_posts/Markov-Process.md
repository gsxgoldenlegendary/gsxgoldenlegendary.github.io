---
title: Markov Process
date: 2021-10-26 13:57:01
tags: Stochastic Process
categories: Mathematics 
mathjax: true
---

# Markov 过程

Markov过程是研究离散事件动态系统状态空间的重要方法,它的原始模型Markov链 ，由俄国数学家A.A.Markov于1907年提出。

<!--more-->

## Markov链的定义和例子

### Markov链

如果对任何一列状态，$i_0,i_1,\cdots,i_{n-1},i,j$，及对任何$n\geqslant 0$，随机过程${X_n,n\geqslant0}$满足Markov性质$$P\{X_{n+1}=j|X_0=i_0,\cdots,X_{n-1}=i_{n-i},X_n=i_n\}=P\{X_{n+1}=j|X_n=i\}$$，则称$X_n$为离散时间Markov链。

### Markov链的一步转移概率

设$X_n$为一离散时间Makov链。给定$X_n$在状态$i$时，$X_{n+1}$处于状态$j$的条件概率$P\{X_{n+1}=j|X_n=i\}$称为Markov链的一步转移概率，并记为$P_{ij}^{n.n+1}$。当这一概率与$n$无关时称该Markov链有平稳转移概率，并记为$P_{ij}$。

### Markov链的n步转移概率矩阵

Markov链的$n$步转移概率矩阵满足$P_{ij}^{(n)}=\sum\limits_{k=0}\limits^\infty P_{ik}P_{kj}^{(n-1)}$，我们约定$P_{ii}^{(0)}=1$，当$j\neq i$时$P_{ij}^{(0)}=0$。

## Markov链的状态分布

### 可达与互达

如果对某一$n\geqslant0$，有$P_{ij}^{(n)}>0$，则称状态$j$是从状态$i$可达的，记作$i\to j$。它表示从状态$i$经过有限步的转移可以到达状态$j$。两个互相可达的状态$i$和$j$则称为互达的，记作$i\leftrightarrow j$。

### 互达性

互达性是等价关系。即
(i)$i\leftrightarrow j$，自反性；
(ii)若$i\leftrightarrow j$，则$j\leftrightarrow i$，对称性；
(iii)若$i\leftrightarrow j$，且$j\leftrightarrow k$，传递性。

### 状态的周期

设$i$为Markov链的一个状态，使$P_{ii}^{(n)}>0$的所有正整数$n(n\geqslant 1)$的最大公约数称作是状态$i$的周期，记作$d(i)$。如果对所有$n\geqslant 1$，都有$P_{ii}^{(n)}=0$，则约定周期为$\infty$；$d(i)=1$的状态则称为是非周期的。

### 状态周期的性质

如果$i\leftrightarrow j$，则$d(i)=d(j)$。

### 周期的基本性质

如果状态$i$有周期$d(i)$，则存在正整数$d(n)$，使得对所有的$n>N$恒有$P_{ii}^{(nd(n))}>0$​。

### 周期的推广性质

如果$P_{ji}^{(m)}>0$，则存在正整数$N$使得对$n>N$恒有$P_{ji}^{(m+nd(i))}>0。

### 非周期不可约Markov链性质

令$\textbf{P}$为不可约、非周期、有限状态Markov链的转移概率阵，则必存在$N$，使得当$n\geqslant N$时，$n$步转移概率阵$\textbf{P}^{(n)}$的所有元素都非零。

### 常返与瞬过

如果 $f_{ii}=1$，我们称状态$i$是常返的，一个非常返的状态称为瞬过的。其中$f_{ij}=\sum\limits_{n=1}^\infty f_{ij}^{(n)},f_{ij}^{(n)}$为首达概率，
$$
f_{ij}^{(0)}=0;f_{IJ}^{(n)}=P\{X_n=j,X_k\neq j,k=1,\cdots,n-1|X_0=i \}.
$$

### 常返与瞬过的充要条件

状态$i$常返的充分必要条件是$\sum\limits_{n=1}^\infty P_{ii}^{(n)}=\infty$。当然与此等价地有，状态$i$是瞬过的当且仅当$\sum\limits_{n=1}^\infty P_{ii}^{(n)}<\infty$。

### 常返与可达的关系

如果$i$是常返的，且$i\leftrightarrow j$，则$j$也是常返的。

### 零常返与正常返

一个常返状态$i$当且仅当$\mu_i=\infty$时称为零常返的，而当且仅当$\mu_i<\infty$时称为正常返的，其中$$\mu=ET_i=\sum\limits_{n=1}^\infty nf_{ii}^{(n)}.$$

## Markov链的极限定理与平稳分布

### Markov链的基本极限定理

1. 若状态$i$是瞬过的或是零常返的，则$$\lim\limits_{n\to\infty} P_{ii}^{(n)}=0.$$
2. 若状态$i$是周期为$d$的常返状态，则$$\lim\limits_{n\to\infty}P_{ii}^{(nd)}=\frac{d}{\mu_i}.$$
3. 当状态$i$是非周期的正常返状态，则$$\lim\limits_{n\to\infty}P_{ii}^{(nd)}=\frac{1}{\mu_i}.$$

### Markov链的平稳分布

Markov链有转移概率阵$\textbf{P}=(P_{ij})$。一个概率分布$\{\pi_i,i\geqslant0\}$如果满足
$$
\pi_j=\sum\limits_{i=0}^\infty \pi_iP_{ij},
$$
则称为这一Markov链的平稳分布。

### 平稳分布的判定

若一个不可约Markov链中的所有状态都是遍历的，则对所有$i,j$，极限
$$
\lim\limits_{n\to\infty}P_{ij}^{(n)}=\pi_j
$$
存在且$\pi=\{\pi_j,j\geqslant0\}$为平稳分布。也即
$$
\sum\limits_{j}\pi_j=1,\pi_j>0,\sum\limits_i\pi_iP_{ij}=\pi_j.
$$
反之，若一个不可约Markov链只存在一个平稳分布，即满足$(4)$式，且这个Markov链的所有状态都是遍历的，则该平稳分布就是这一Markov链的极限分布，即对任何$i$有
$$
\lim\limits_{n\to\infty}P_{ij}^{(n)}=\pi_j.
$$

## 连续时间Markov链

### 连续时间Markov链

若对所有$s,t\geqslant0$和任何非负整数$i,j,x(u),0\leqslant u<s$，随机过程$X(t),t\geqslant0$满足
$$
P\{X(t+s)=j|X(s)=i,X(u)=x(u),0\leqslant u<s\}=P\{X(t+s)=j|X(s)=i\},
$$
则称为连续时间Markov链。

### 连续时间Markov链的联合分布

连续时间Markov链的转移概率$P_{ij}(i)$和$p_i$完全确定了过程的所有联合分布。

### 连续时间Markov链的转移概率函数

函数$P_{ij}(t)$能够作为无瞬即转移的Markov过程的转移概率函数的充分必要条件是它满足：
$$
P_{ij}(t)\geqslant0,\sum\limits_jP_{ij}(t)=1,
$$

$$
P_{Ij}(t+\tau)=\sum_kP\{X(t+\tau)=j,X(\tau)=k|X(0)=i\}=\sum\limits_kP_{ik}(\tau)P_{kj}(t),
$$

$$
\lim\limits_{\tau\downarrow0}P\{X(t+\tau)=i|X(t)=i\}=\lim\limits_{\tau\downarrow0}P_{ii}(\tau)=1.
$$

## 难题集萃

### Markov过程的转移概率矩阵

记$Z_i,i=1,2,\cdots$为一串独立同分布的离散随机变量。$$P\{Z_1=k\}=p_k\geqslant0,k=0,1,2,\cdots,\sum\limits_{k=0}^\infty p_k=1.$$记$X_n=Z_n,n=1,2\cdots$。试求过程$X_n$的转移概率矩阵。

解：
$$
\textbf{P}=(p_{ij})_{\infty\times\infty}.
$$



$$
p_{ij}=\sum\limits_{i=0}^\infty p_ip_j=p_j.
$$

未完待续

