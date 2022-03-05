---
title: Hypothesis Testing
date: 2022-01-07 08:19:06
tags: Mathematical Statistics
categories: Mathematics 
mathjax: true
---

假设检验，又称统计假设检验，是用来判断样本与样本、样本与总体的差异是由抽样误差引起还是本质差别造成的统计推断方法。显著性检验是假设检验中最常用的一种方法，也是一种最基本的统计推断形式，其基本原理是先对总体的特征做出某种假设，然后通过抽样研究的统计推理，对此假设应该被拒绝还是接受做出推断。

<!--more-->

# 问题提法与基本概念

## 功效函数

设总体分布包含若干个未知参数$\theta_1,\cdots,\theta_k$，$H_0$是关于这些参数的一个原假设，设有了样本$X_1,\cdots,X_n$，而$\Phi$是基于这些样本而对$H_0$所做的一个检验，则称检验$\Phi$的功效函数为
$$
\beta_\Phi(\theta_1,\cdots,\theta_k)=P_{\theta_1,\cdots,\theta_k}(在检验\Phi 之下，H_0被否定).
$$

## 检验的水平

设$\Phi$是原假设$H_0$的一个检验，$\beta_\Phi(\theta_1,\cdots,\theta_k)$为其功效函数，$\alpha$为常数$(0\leqslant\alpha\leqslant 1)$。如果
$$
\beta_\Phi(\theta_1,\cdots,\theta_k)\leqslant\alpha(\forall(\theta_1,\cdots,\theta_k)\in H_0),
$$
则称$\Phi$为$H_0$的一个水平为$\alpha$的检验。

# 重要参数检验

## 正态总体均值的检验

### 方差已知

$$
\frac{\bar X_n-\mu_0}{\frac\sigma{\sqrt n}}\sim N(0,1).
$$



### 方差未知

$$
\frac{\bar X_n-\mu_0}{\frac\S{\sqrt n}}\sim t_{n-1}.
$$



## 两个正态总体均值差的检验

### 方差已知

$$
\frac{\bar X-\bar Y-(\mu_1-\mu_2)}{\sqrt{\frac {\sigma_1^2} {n_1}+\frac{\sigma_2^2} {n_2}}}\sim N(0,1).
$$



### 方差未知且相等

$$
\frac{\bar X-\bar Y-(\mu_1-\mu_2)}{\sqrt\frac{(n_1-1)S_1^2+(n_2-1)S_2^2}{n_1+n_2-2}\sqrt{\frac 1 {n_1}+\frac1 {n_2}}}\sim t_{n_1+n_2-2}.
$$





## 正态分布方差的检验

### 单总体

$$
\frac{(n-1)S_1^2}{\sigma_1^2}\sim\chi_{n-1}^2
$$



### 双总体

$$
\frac{\frac{S_1^2}{\sigma_1^2}}{\frac{S_2^2}{\sigma_2^2}}\sim F_{n_1-1.n_2-1}.
$$

# 拟合优度检验

$$
Z=\sum\frac{(理论值-经验值)^2}{理论值}=\sum_{i=1}^k \frac{(np_i-\nu_i)^2}{np_i}.
$$

## 理论分布完全已知且仅取有限个值的情况

如果原假设$H_0$成立，则在样本大小$n\to\infty$时，$Z$的分布趋向于自由度为$k-1$的$\chi^2$分布，即$\chi_{k-1}^2$。

## 理论分布仅取有限个值但不完全已知的情况

在一定的条件下，若原假设$H_0$成立，则在样本大小$n\to\infty$时，$Z$的分布趋向于自由度为$k-1-r$的$\chi^2$分布，即$\chi_{k-1-r}^2$。

## 对列联表的应用

$$
V_n=\frac{n(n_{11}n_{22}-n_{12}n_{21})^2}{n_{1\cdot}n_{2\cdot}n_{\cdot 1}n_{\cdot 2}}\sim\chi_1^2.
$$

