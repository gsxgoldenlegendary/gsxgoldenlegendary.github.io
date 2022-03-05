---
title: Parameter Estimation
date: 2021-11-25 10:26:36
tags: Mathematical Statistics
categories: Mathematics 
mathjax: true
---

数理统计学使用概率论和数学的方法，研究通过试验或观察收集带有随机误差的数据，并在统计模型之下，对这种数据进行统计分析，以对所研究的问题做出统计推断。

<!--more-->

# 数理统计学的基本概念

## 总体

总体是指与所研究的问题有关的对象（个体）的全体构成的集合。

## 样本

样本是按一定的规定从总体抽出的一部分个体。所谓“按一定的规定”，是指总体中的每一个个体有同等的被抽出的机会。

## 统计量

完全由样本所决定的量叫做统计量。

# 矩估计，极大似然估计和贝叶斯估计

## 矩估计

设总体分布为$f(x;\theta_1,\cdots,\theta_k)$，则它的矩（以连续型的原点矩为例）
$$
a_m-\int_{-\infty}^\infty x^mf(x;\theta_1,\cdots,\theta_k)\mathrm dx
$$
依赖于$\theta_1,\cdots,\theta_k$。另一方面，至少在样本大小$n$较大时，$\alpha_m$又应接近于样本原点矩$a_m$。于是
$$
\alpha_m=\alpha_m(\theta_1,\cdots,\theta_k)\approx a_m=\frac {\sum_{i=1}^n X_i^m} n
$$
取$m=1,\cdots,k$，并将上面的近似式改成等式，就得到一个方程组：
$$
\alpha(\theta_1,\cdots,\theta_k)=a_m(m=1,\cdots,k).
$$
解此方程组，得其根$\hat\theta_i=\hat\theta_i(X_1,\cdots,X_n)(i=1,\cdots,k)$，就以$\hat\theta_i$作为$\theta_i$的估计（$i=1,\cdots,k$）。如果要估计的是$\theta_1,\cdots,\theta_k$的某函数$g(\theta_1,\cdots,\theta_k)$，则用
$$
\hat g=\hat (X_1,\cdots,X_n)=g(\hat\theta_1,\cdots,\hat\theta_k)
$$
去估计它。

## 极大似然估计

设总体分布为$f(x;\theta_1,\cdots,\theta_k)$，$X_1,\cdots,X_n$为自这个总体中抽出的样本，则样本$(X_1,\cdots,X_n)$的分布为
$$
f(x_1;\theta_1,\cdots,\theta_k)f(x_2;\theta_1,\cdots,\theta_k)\cdots f(x_n;\theta_1,\cdots,\theta_k),
$$
记为$L(x_1,\cdots,x_n;\theta_1,\cdots,\theta_k)$。

用满足条件
$$
L(X_1,\cdots,X_n;\theta_1^*,\cdots,\theta_k^*)=\max_{\theta_1,\cdots,\theta_k}L(X_1,\cdots,X_n;\theta_1,\cdots,\theta_k)
$$
的$(\theta_1^*,\cdots,\theta_k^*)$去作为$(\theta_1,\cdots,\theta_k)$的估计值。如果要估计的是$g(\theta_1,\cdots,\theta_k)$，则$g(\theta_1^*,\cdots,\theta_k^*)$是它的极大似然估计。

# 点估计的优良性准则

## 无偏性

设某统计总体的分布包含未知参数$\theta_1,\cdots,\theta_k$，$X_1,\cdots,X_n$是从该总体中抽出的样本，$\hat g(X_1,\cdots,X_n)$是$g(\theta_1,\cdots,\theta_k)$的一个估计量。如果对任何可能的$(\theta_1,\cdots,\theta_k)$，都有
$$
E_{\theta_1,\cdots,\theta_k}(\hat g(X_!,\cdots,X_n))=g(\theta_1,\cdots,\theta_k),
$$
则称$\hat g$是$g(\theta_1,\cdots,\theta_k)$的一个无偏估计量。

# 区间估计

## 置信系数与置信界

#### 置信系数

给定一个很小的数$\alpha>0$，如果对参数$\theta$的任何值，概率
$$
P_\theta(\hat\theta_1(X_1,\cdots,X_n)\leqslant\theta\leqslant\hat\theta_1(X_1,\cdots,X_n))
$$
都等于$1-\alpha$，则称区间估计$[\hat\theta_1,\hat\theta_2]$的置信系数为$1-\alpha$。

### 置信上界

给定一个很小的数$\alpha>0$，如果对参数$\theta$的任何值，概率
$$
P_\theta(\bar\theta(X_1,\cdots,X_n)\geqslant\theta)
$$
都等于$1-\alpha$，则称$\bar \theta$为$\theta$的一个置信系数为$1-\alpha$的置信上界。

### 置信下界

给定一个很小的数$\alpha>0$，如果对参数$\theta$的任何值，概率
$$
P_\theta(\underline\theta(X_1,\cdots,X_n)\leqslant\theta)
$$
都等于$1-\alpha$，则称$\underline \theta$为$\theta$的一个置信系数为$1-\alpha$的置信下界。



## 正态总体样本均值、样本方差的分布

### 一般总体样本均值、样本方差的性质

$$
E\bar X=\mu,D(\bar X)=\frac{\sigma^2} n,
$$

$$
E S^2=D(X)=\sigma^2
$$

### 正态总体样本均值、方差的分布

设$X_1,\cdots,X_n$是来自正态总体$N(\mu,\sigma^2)$的样本，$\bar X$与$S$分别是样本均值与样本标准差，则
$$
\bar X\sim N(\mu,\frac {\sigma^2} n),或\frac{\bar X-\mu}{\frac \sigma{\sqrt n}}\sim N(0,1).
$$

$$
\frac {(n-1)S^2}{\sigma^2}\sim \chi_{n-1}^2.
$$

$\bar X$与$S^2$相互独立。
$$
\frac{\bar X-\mu}{\frac S {\sqrt n}}\sim t_{n-1}.
$$
设$X_1,\cdots,X_n$是来自正态总体$N(\mu_1,\sigma_1^2)$的样本，$Y_1,\cdots,Y_n$是来自正态总体$N(\mu_2,\sigma_2^2)$的样本，且$X$与$Y$相互独立，$\bar X,\bar Y$分别表示样本均值，$S_1^2,S_2^2$分别表示样本方差，则：
$$
\frac{\frac{S_1^2}{\sigma_1^2}}{\frac{S_2^2}{\sigma_2^2}}\sim F_{n_1-1.n_2-1}.
$$
当$\sigma_1=\sigma_2$时，
$$
\frac{\bar X-\bar Y-(\mu_1-\mu_2)}{\sqrt\frac{(n_1-1)S_1^2+(n_2-1)S_2^2}{n_1+n_2-2}\sqrt{\frac 1 {n_1}+\frac1 {n_2}}}\sim t_{n_1+n_2-2}.
$$


## 枢轴变量法

1. 找一个与要估计的参数$g(\theta)$有关的统计量$T$，一般是其一个良好的点估计。

2. 设法找出$T$和$g(\theta)$的某一函数$S(T,g(\theta))$，其分布$F$要与$\theta$无关。

3. 对任何常数$a<b$，不等式$a\leqslant S(T,g(\theta))\leqslant b$要能改写为等价的形式$A\leqslant g(\theta)\leqslant B$，$A,B$只与$T,a,b$有关，而与$\theta$无关。

4. 取分布$F$的上$\frac \alpha 2$分位点$w_{\frac \alpha 2}$和上$1-\frac \alpha 2$分位点$w_{1-\frac \alpha 2}$，则有
   $$
   P(w_{\frac \alpha 2}\leqslant S(T,g(\theta))\leqslant w_{1-\frac\alpha 2})=1-\alpha.
   $$
   将
   $$
   w_{\frac \alpha 2}\leqslant S(T,g(\theta))\leqslant w_{1-\frac\alpha 2}
   $$
   改写成$A\leqslant g(\theta)\leqslant B$的形式，则$[A,B]$就是$g(\theta )$的一个置信系数为$1-\alpha$的区间估计。

