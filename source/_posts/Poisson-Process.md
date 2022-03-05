---
title: Poisson Process
date: 2021-10-26 14:02:09
tags: Stochastic Process
categories: Mathematics 
mathjax: true
---

# Poisson 过程

Poisson过程是一系列离散事件的模型，事件之间的平均时间是确定的，但事件发生的确切时间是随机的，一个事件的到来与之前的事件无关。

<!--more-->

## Poisson过程

### Poisson过程

一个整数值随机过程$\{N(t),t\geqslant0\}$满足下述三个条件就称作强度为$\lambda>0$的Poisson过程：

1. $N(0)=0$；
2. $N(t)$是独立增量过程；
3. 对任何$t>0$，$s\geqslant0$增量$N(s+t)-N(t)$服从参数为$\lambda t$的Poisson分布，即$$P\{N(s+t)-N(t)=k\}=\frac{(\lambda t)^ke^{-\lambda t}}{k!},k=0,1,\cdots$$。

满足假定1~4的随机过程$N(t)$为Poisson过程。

1. 在不相交区间中事件发生的数目相互独立，也即对任何整数$n=1,2,\cdots$，设时刻$t_0=0<t_1<t_2<\cdots<t_n$，增量$$N(t_1)-N(t_0),N(t_2)-N(t_1),\cdots,N(t_n)-N(t_{n-1})$$相互独立；
2. 对任何时刻$t$和正数$h$，随机变量（增量）$N(t+h)-N(t)$的分布只依赖于区间长度$h$而不依赖时刻$t$；
3. 存在正整数$\lambda$当$h\downarrow 0$时，使在长度为的小区间中事件至少发生一次的概率$$P\{N(t+h)-N(t)\geqslant1\}=\lambda h+\omicron(h)$$；
4. 在小区间$(t,t+h]$发生两个或两个以上事件的概率为$\omicron(h)$（可以忽略不计），即当$h\downarrow 0$，$P\{N(t+h)-N(t)\geqslant2\}=\omicron (h)$。

## 与Poisson过程相联系的若干分布

### 间隔时间和等待时间的分布

第$n-1$次与第$n$次事件间的间隔时间记作$X_n$，而$W_n=\sum\limits_{i-1}\limits^nX_i$为第$n$次事件的到达或等待时间，则$X_n,n=1,2,\cdots$是均值为$\frac{1}{\lambda}$的独立同分布的指数随机变量，$W_n$服从参数为$n$，和$\lambda$的$\Gamma$分布。

### 等待时间的联合分布

若$N(t),t\geqslant 0$为Poisson过程，则给定$N(t)=n$下等待时间$W_1,\cdots,W_n$的联合密度为$$f_{W_1,\cdots,W_n|N(t)=n}(\omega_1.\cdots,\omega_n|n)=\frac{n!}{t^n},0<\omega_1<\cdots<\omega_n\leqslant t$$。

## Poisson过程的推广

### 更新过程

如果$X_i,i=1,2,\cdots$为一非负的随机变量，它们独立同分布，分布函数为$F(x)$。记$W_0=0,W_n=\sum\limits_{i=1}\limits^nX_i$，$W_i$表示第$n$次事件发生的时刻，则称$N(t)=max\{n:W_n\leqslant t\}$为更新过程。

### 更新过程的分布

更新过程$N(t)$的分布$P\{N(t)=n\}=F^{(n)}(t)-F^{(n+1)}(t)$，而更新函数$m(t)=\sum\limits_{n=1}\limits^\infty F^{(n)}(t)$，其中$F^{(n)}(t)$为$F(t)$的$n$重卷积，$F(t)$即为$X_i$的分布函数。

## 难题集萃

### 多个独立Poisson过程

设某路口蓝车，白车和黄车的到达次数分别为强度$\lambda_1,\lambda_2,\lambda_3$的Poisson过程，且相互独立。试求在相继到达的两辆蓝车之间，恰有$k$辆车到达的概率。

易知蓝车首先到达的概率为$p=\frac{\lambda_1}{\lambda_1+\lambda_2+\lambda_3}$，不是蓝车的概率为$1=p$，认为蓝车到达为“成功”，否则为“失败”，则两次蓝车之间到达车辆分布服从几何分布，即$$P(N=k)=(1-p)^kp=\frac{\lambda_1(\lambda_2+\lambda_3)^k}{(\lambda_1+\lambda_2+\lambda_3)^{k+1}}$$。

### 冲击模型

记$N(t)$为某系统到某时刻$t$受到的冲击次数，它是参数为$\lambda$ 的Poisson过程。设第$k$次冲击对系统的损害大小$Y_k$服从参数为$\mu$的指数分布，$Y_k,𝑘=1,2,· · ·$，独立同分布。记$X(t)$为系统所受到的总损害。当损害超过一定的极限$\alpha$时系统不能运行，寿命终止，记$T$为系统寿命。试求该系统的平均寿命$ET$。

解：
$$
ET=\int_0^\infty tf(t)\mathrm{d}t=\int_0^\infty(\int_0^tf(t)\mathrm{d}s)\mathrm{d}t
$$

$$
=\int_0^\infty(\int_t^\infty f(t)\mathrm{d}t)\mathrm{d}s=\int_0^\infty P(T>t)\mathrm{d}t
$$

$$
P(T>t)=P(X(t)\leqslant\alpha)=P(\sum\limits_{i=1}\limits^{N(t)}Y_i\leqslant\alpha)
$$

$$
=\sum\limits_{n=0}\limits^\infty P(\sum\limits_{i=1}\limits^{N(t)}Y_i\leqslant\alpha|N(t)=n)P(N(t)=n)
$$

$$
\therefore ET=\int_0^\infty 1\cdot P(N(t)=0)+\int_0^\infty\sum\limits_{n=0}\limits^\infty P(\sum\limits_{i=1}\limits^{n}Y_i\leqslant\alpha)P(N(t)=n)
$$

$$
=\frac{1}{\lambda}+\int_0^\infty\sum\limits_{n=1}\limits^\infty(\int_0^\alpha\frac{\mu(\mu y)^{n-1}}{(n-1)!}e^{-\mu y}\mathrm{d}y)\frac{(\lambda t)^n e^{-\lambda t}}{n!}\mathrm{d}t
$$

$$
=\frac{1}{\lambda}+\int_0^\alpha\sum\limits_{n=1}\limits^\infty(\int_0^\infty \frac{(\lambda t)^n e^{-\lambda t}}{n!}\mathrm{d}t)\frac{\mu(\mu y)^{n-1}}{(n-1)!}e^{-\mu y}\mathrm{d}y
$$

$$
=\frac{1}{\lambda}+\int_0^\alpha\sum\limits_{n=1}^\limits\infty\frac{\Gamma(n)}{\lambda n!}\frac{\mu(\mu y)^{n-1}}{(n-1)!}e^{-\mu y}\mathrm{d}y
$$

$$
=\frac{1}{\lambda}+\frac{1}{\lambda}\int_0^\alpha\sum\limits_{n=1}^\limits\infty\frac{\mu(\mu y)^{n-1}}{(n-1)!}e^{-\mu y}\mathrm{d}y
$$

$$
=\frac{1}{\lambda}+\frac{1}{\lambda}\int_0^\alpha\mu\mathrm{d}y=\frac{\mu\alpha+1}{\lambda}
$$

注意：$n$个同分布的参数为$\lambda$的指数随机变量的和服从参数为$n,\lambda$的$\Gamma$分布。

### 非齐次Poisson过程的事件时间间隔

令$N(t)$是强度为$\lambda(t)$的非齐次Poisson过程，$X_1,X_2,\cdots$为事件间的时间间隔，则$X_i$不独立。

解：
$$
𝑃 (𝑋_2 > 𝑡|𝑋_1 = 𝑠) = 𝑃 (𝑁(𝑡 + 𝑠) − 𝑁(𝑠) = 0|𝑁(𝑠) = 1) =𝑃(𝑁(𝑡 + 𝑠) − 𝑁(𝑠) = 0) = 𝑒^{-\int_s^{t+s}\lambda(s)\mathrm{d}s}
$$
由于$𝑃(X_2>t|X_1=s)$与$s$有关，故$X_1$与$X_2$不独立，故$X_i$不独立。

注意：非齐次Poisson过程的$N(t)$也是独立增量过程。

### 更新过程的等待时间

设$N(t)$为更新过程，则$\{N(t)\leqslant k\}\nLeftrightarrow\{W_k\geqslant t\}$。

解：第$k$次更新发生在$t$时刻之前，第$k+1$次更新发生在$t$时刻之后，此时$W_k<k$，且$N(t)\leqslant k$。

