---
title: Probability of Events
date: 2021-10-30 12:47:44
tags: Probability Theory 
categories: Mathematics 
mathjax: true
---

# 事件的概率

概率亦称“或然率”、“机率”。它反映随机事件出现的可能性大小的量度。

<!--more-->

## 概率是什么

### 古典概率

设一个试验有$N$个等可能的结果，而事件$E$恰包含其中的$M$个结果，则事件$E$的概率，记为$P(E)$，定义为$P(E)=\frac{M}{N}$。

## 事件的运算、条件概率与独立性

### 概率的加法定理

若干个互斥事件和的概率，等于各事件的概率之和，即
$$
P(A_1+A_2+\cdots)=P(A_1)+P(A_2)+\cdots.
$$

### 条件概率

设有两个事件$A,B$，而$P(B)\neq 0$。则“在给定$B$发生的条件下$A$的条件概率”，记为$P(A|B)$，定义为
$$
P(A|B)=\frac{P(AB)}{P{B}}.
$$

### 事件的独立性

设$A_1,A_2,\cdots$为有限或无限个事件，如果从其中任意取出有限个$A_{i_1},A_{i_2},\cdots,A_{i_m}$，都成立
$$
P(A_{i_1}A_{i_2}\cdots A_{i_m})=P(A_{i_1})P(A_{i_2})\cdots P(A_{i_m}),
$$
则称事件$A_1,A_2,\cdots$相互独立，或简称独立。

### 概率的乘法定理

若干个独立事件$A_i,\cdots,A_n$之积的概率，等于各事件概率的乘积：
$$
P(A_1\cdots A_n)=P(A_1)\cdots P(A_n).
$$

### 全概率公式

$B_1,B_2,\cdots$为一个完备事件群，对任意事件$A$，有全概率公式：
$$
P(A)=P(B_1)P(A|B_1)+P(B_2)P(A|B_2)\cdots.
$$

### 贝叶斯公式

$B_1,B_2,\cdots$为一个完备事件群，对任意事件$A$，有贝叶斯公式：
$$
P(B_i|A)=\frac{P(AB_i)}{P(A)}=\frac{P(B_i)P(A|B_i)}{\sum\limits_jP(B_j)P(A|B_j)}.
$$
