---
title: Graph Theory Theorem
date: 2022-01-03 10:27:07
tags: Graph Theory
categories: Mathematics 
mathjax: true
---

图论是应用数学的一个分支，它是反映一些元素之间关系的数学模型。图论的概念于成果以及它的应用非常广泛，既有来自生产实践的许多应用问题，也有许多来自其他学科的理论问题。这里介绍图论的基本定理。

<!--more-->

# 图的基本概念

## Euler定理

任给无向图$G$，
$$
\sum\limits_{v\in V(G)}\deg(v)=2\varepsilon(G).
$$

## 二分图的充要条件

图$G$是二分图，当且仅当$G$中无奇圈。

## 有向图的Euler定理

$$
\sum\limits_{v\in V(D)}\deg^+(v)=\sum\limits_{v\in V(G)}\deg^-(v)=\varepsilon(G).
$$

# 树

## 树的充要条件

设$G=(V(G),E(G))$是简单无向图，则一下命题等价：

1. $G$是树。
2. $G$的任意两个顶点之间有且仅有一条轨道。
3. $G$不含圈，且$\varepsilon(G)=\nu(G)-1$。
4. $G$是连通图，且$\varepsilon(G)=\nu(G)-1$。
5. $G$是连通图，且删去任意一条边都不连通。
6. $G$不含圈，且添加一条边后恰好含一个圈。

## 树叶的个数

任一非平凡树$T$至少有两片树叶。

## 树与连通图

每个连通图都有生成树。

## Cayley定理

设$G$是连通图，$e=uv\in E(G)$且不是环，则
$$
\tau(G)=\tau(G-e)+\tau(G\cdot e).
$$

## 完全图的生成树

$$
\tau(K_n)=n^{n-2}.
$$

## 二叉树的性质

二叉树有以下性质：

1. 第$i$层的顶点数最多是$2^i$；
2. 深度为$h$的二叉树最多有$2^{h+1}-1$个顶点；
3. 设二叉树出度为$2$的顶点数为$n_2$，树叶数为$n_0$，则有$n_0=n_2+1$；
4. 包含$n$个顶点的二叉树的高度至少为$\log(n+1)-1$。

# 图的连通性

## Menger定理顶点版本

给定简单图$G$中两个不相邻的顶点$u,v$，$G$中两两无公共内顶的$uv$-轨道的最大数量等于最小$uv$-割集中的顶点数，即：
$$
p(u,v)=c(u,v).
$$

## Whitney定理

任给简单图$G$，都有：
$$
\kappa(G)=\min\{p(u,v)|u,v\in V(G),u\neq v\}.
$$

## 扇形引理

假设简单图$G$是$k$-连通图，在$G$中增加一个新的顶点$y$，并且在$G$中任意选取至少$k$个顶点，将$y$与这些选取的顶点各连一条边，得到的图记为$H$，则$H$也是$k$-连通图。

## Dirac定理

设$S$是$k$-连通图$G$中的$k$元顶点子集，$k\geqslant 2$，则$G$中存在一个圈$C$，使得$S$中所有顶点都在$C$上。

## Menger定理边版本

给定简单图$G$中两个不相邻的顶点$u,v$，$G$中两两无公共边的$uv$-轨道的最大数量等于最小$uv$-边割集中的顶点数，即：
$$
p'(u,v)=c'(u,v).
$$

## 两种连通度的关系

假定$G$是简单连通图，则有：
$$
\kappa(G)\leqslant\kappa'(G)\leqslant\delta(G).
$$


## 割顶的性质

设$G$是连通图，$v\in V(G)$，则下述命题等价：

1. $v$是$G$的割顶；

2. 存在与$v$不同的两个顶点$u,w\in V(G)-\{v\}$，使得$v$在每一条从$u$到$w$的轨道上；

3. 存在$V(G)-\{v\}$的一个划分
   $$
   V(G)-\{v\}=U\cup W,U\cap W=\emptyset,u\neq\emptyset,W\neq\emptyset,
   $$
   使得任给$u\in U,w\in  W$，$v$在每一条从$u$到$w$的轨道上。

## 桥的性质

设$G$是连通图，$e\in E(G)$，则下述命题等价：

1. $e$是$G$的桥；

2. $e$不在$G$的任一圈上；

3. 存在$u,w\in V(G)$，使得$e$在每一条从$u$到$w$的轨道上；

4. 存在$V(G)$的一个划分
   $$
   V(G)=U\cup W,U\cap W=\emptyset,u\neq\emptyset,W\neq\emptyset,
   $$
   使得任给$u\in U,w\in  W$，$e$在每一条从$u$到$w$的轨道上。

## 块的性质

设$G$是连通图，$\nu(G)\geqslant3$，则下述命题等价：

1. $G$是块。
2. 任给$u,v\in V(G)，u\neq v$，$u$与$v$在$G$的同一个圈上。
3. 任给$u\in V(G)$，$e\in E(G)$，$u$与$e$在$G$的同一个圈上。
4. 任给$e_1,e_2\in E(G)，e_1\neq e_2$，$e_1$与$e_2$在$G$的同一个圈上。
5. 任给$u,v\in V(G)，u\neq v,e\in E(G)$，存在连接$u$与$v$的轨道$P(u,v)$，使得$e$在$P(u,v)$上，即$e\in E(P(u,v))$。
6. 任给三个不同的顶点$u,v,w\in V(G)$，存在连接$u$与$v$的轨道$P(u,v)$，使得$w$在轨道$P(u,v)$上。
7. 任给三个不同的顶点$u,v,w\in V(G)$，存在连接$u$与$v$的轨道$P(u,v)$，使得$w$不在轨道$P(u,v)$上。

# 平面图

## 可嵌入平面与可嵌入球面

图$G$可嵌入平面，当且仅当$G$可嵌入球面。

## 平面嵌入的外部面

设$v$是平面图$G$的顶点，则存在$G$的一个平面嵌入，使得$v$在这个嵌入的外部面上。

## 面的度数与边数的关系

任给平面图$G$，
$$
\sum\limits_{f\in F(G)}\deg(f)=2|E(G)|.
$$

## Euler公式

设$G$是联通平图，有$\nu$个顶点，$\varepsilon$条边，$\phi$个面，则
$$
\nu-\varepsilon+\phi=2.
$$

## 平面图边数上界

若$G$是$\nu\geqslant3$的连通平面图，则$\varepsilon\leqslant3\nu-6$

## 连通简单平面图顶点最小度的上界

若$G$是连通简单平面图，则$\delta\leqslant5$。

## 极大平面图的充要条件

$\nu\geqslant3$的平面图$G$是极大平面图，当且仅当$G$的平面嵌入的每个面都是三角形。



## 极大平面图顶点最小度的下界

若$G$是$\nu\geqslant3$的平面图，则$\delta \geqslant 3$。

## Kuratowsky定理

图$G$是平面图，当且仅当$G$中不含与$K_5$或$K_{3,3}$同胚的子图。

## 简单图厚度估计

对$\nu\geqslant3$阶简单图$G$的厚度$\theta(G)$，有以下估计式：

1. $$
   \theta(G)\geqslant\lceil\frac\varepsilon{3\nu-6}\rceil.
   $$

   

2. 若连通图$G$中没有$3$阶圈，则
   $$
   \theta(G)\geqslant\lceil\frac\varepsilon{2\nu-4}\rceil.
   $$

3. $$
   \theta(K_\nu)\geqslant\lceil\frac{\nu+7}6\rceil.
   $$

# 匹配理论

## 最大匹配与可增广轨道

$M$是$G$的最大匹配，当且仅当$G$中没有关于$M$的可增广轨道。

## Hall定理

设$G$是二分图，其顶点集合划分为$V(G)=X\cup Y,X\cap Y=\emptyset$，则$G$中存在将$X$中顶点都许配的匹配，当且仅当任给$S\subset X$，都有$|N(S)|\geqslant |S|$，其中，$N(S)$是与$S$中顶点相邻的顶点构成的集合，简称为$S$的邻顶集合。

## 覆盖数与匹配数

假设$C$是图$G$的覆盖，$M$是图$G$的匹配，则$|C|\geqslant|M|$。

## 最小覆盖与最大匹配

若图$G$存在覆盖$C$与匹配$M$，使得$|C|=|M|$，则$C$是最小覆盖，$M$是最大匹配。

## König-Egerváry定理

设$G$是二分图，则$G$的匹配数等于其覆盖数，即$\alpha(G)=\beta(G)$。

## Tutte定理

$G$有完备匹配，当且仅当任给$S\subset V(G)$，都有$\omicron(G-S)\leqslant|S|$。

## Peterson定理

无桥的三次正则图有完备匹配。

# Euler图与Hamilton图

## 无向Euler图的等价条件

设$G$是连通图，则下面三个命题等价：

1. $G$是Euler图；
2. $G$的每个顶点的度数都是偶数；
3. $G$可以表示成无公共边的圈之并。

## 有向Euler图的等价条件

设$D$是有向图，则下面三个命题等价：

1. $D$是Euler图；
2. $\forall v\in V(D),\deg^+(v)=\deg^-(v)$；
3. $D$可以表示成无公共边的有向圈之并。

## Hamilton图的必要条件

设$G$是Hamilton图，则对$V(G)$的每个非空真子集$S$，均有$\omega(G-S)\leqslant|S|$，其中$\omega(\cdot)$是连通片的个数。

## Dirac定理

设$G$是简单图，且$\nu(G)\geqslant3,\delta(G)\geqslant\frac{\nu(G)}2$，则$G$是Hamilton图。

## 闭包的确定性

$c(G)$是唯一确定的。

## Hamilton图与闭包

简单图$G$是Hamilton图，当且仅当它的闭包$c(G)$是Hamilton图。

## Ore定理

设$\nu(G)\geqslant3$，对$G$的任意一对顶点$u,v$，若$\deg(u)+\deg(v)\geqslant\nu(G)-1$，则$G$有Hamilton轨道；若$\deg(u)+\deg(v)\geqslant\nu(G)$，则$G$有Hamilton圈。

# 图的着色

## 顶色数的上界

对任何图$G$，$\chi(G)\leqslant\Delta(G)+1$。

## Brooks定理

设$\nu\geqslant3$阶连通图$G$不是完全图也不是奇圈，则 $\chi(G)\leqslant\Delta(G)$。

## 二分图的边色数

若$G$是二分图，则$\chi'(G)=\Delta(G)$。

## Vizing定理

若$G$是简单图，则$\chi'(G)=\Delta(G)$或$\Delta(G)+1$。

## 二分图的匹配划分

设$G$是二分图，$\varepsilon=|E(G)|,\Delta\leqslant p$，则存在$G$的$p$个不相交的匹配$M_1,M_2,\cdots,M_p$，使得
$$
E(G)=\mathop\cup\limits_{i=1}^p M_i,
$$


且对$i\leqslant i\leqslant p$，
$$
\lfloor\frac\varepsilon p\rfloor\leqslant|M_i|\leqslant\lceil\frac\varepsilon p\rceil.
$$

## 连通平面图的对偶图的性质

设$G*$是连通平面图$G$的对偶图，$n^*,m^*,\phi^*$和$n,m,\phi$分别是$G*$和$G$的顶点数、边数和面数，则

1. $$
   n^*=\phi,m^*=m,\phi^*=n
   $$

   

2. 设$G$的顶点$f^*$与$G'$的面$f$对应，则$\deg_{G^*}(F^*)=\deg_G(f)$。

## 六色定理

任何平面图都是可$6$-顶点着色的。

## 五色定理

任何平面图都是可$5$-顶点着色的。

# 有向图

## 强连通的充要条件

$D$是强连通有向图当且仅当$D$中存在有向生成回路，即存在含有$D$中所有顶点的有向回路。

## 连通无向图的定向

连通无向图$G$可以定向成强连通有向图，当且仅当$G$中没有桥。

## 单连通的局部可达

若$D$单连通，则$\forall S\subset V(D),S\neq \emptyset$，都存在顶点$v\in S$，$v$可达$S$中所有的顶点。

## 单连通的充要条件

$D$是单连通有向图，当且仅当$D$中存在有向生成路径。

## Roy-Gallai定理

有向图$D$中含有长度为$\chi(G)-1$的有向轨道，其中$G$是$D$的底图。

## 王的得分

竞赛图中得分最多的顶点是王。

## 王唯一的充要条件

竞赛图$D$中$v$是唯一的王，当且仅当$v$的得分是$\nu-1$，其中$\nu=|V(D)|$。

## 强连通竞赛图的有向圈

假定$\nu\geqslant3$阶竞赛图是强连通的，则任给$3\leqslant k\leqslant\nu$，$D$中每个顶点都在某个$k$阶有向圈中。

## 严格有向图最长轨道的下界

设$P(u_0,v_0)$是严格有向图$D$中的最长有向轨道，则其长度
$$
|E(P(u_0,v_0))|\geqslant\max\{\delta^-,\delta^+\}.
$$
其中，$\delta^-,\delta^+$分别为$D$的最小入度与最小出度。

## 有向Hamilton图的充分条件

设$D$是$\nu$阶严格有向图，若
$$
\min\{\delta^-,\delta^+\}\geqslant\frac\nu 2\geqslant1,
$$
则$D$是有向Hamilton图。

# 网络流理论

## 流量与截

设$f$是网络$N=(D,s,t,c)$的流函数，$(S,\overline S)$是其一个截，则有
$$
\mathrm {Val}(f)=\sum_{e\in(S,\overline S)}f(e)-\sum_{e\in(\overline S,S)}f(e).
$$

## 最大流与最小截

设$f$是网络$N=(D,s,t,c)$的流函数，$(S,\overline S)$是其一个截，若$\mathrm{Val}(f)=C(S,\overline S)$，则$f$是最大流，$(S,\overline S)$是最小截。

## 容量有上下界的网络的可行流

给定网络$N(D,s,t,b,c)$，其伴随网络为$N'=(D',s',t',c')$，则$N$中存在可行流，当且仅当$N'$中最大流使得任给$v\in V(D)$，边$(s'v)$都满载，即若$N'$的最大流为$f’$有$f'((s',v))=c'((s',v))$。

## 有供需需求的网络的可行流

给定有供需约束的网络$N+(D,X,Y,\sigma,\rho,c)$。$N$有可行流的充要条件是：任给$S\subset V(D)$，都满足
$$
C((S,\overline S))\geqslant \rho(Y\cap\overline S)-\sigma(X\cap \overline S).
$$

# 图矩阵与图空间

## 线性子空间的判定

设$V$是数域$F$上的线性空间，$V'\subset V$且$V'\neq\emptyset$。若$V'$中任意两个向量的线性组合仍属于$V’$则$V'$是$V$的线性子空间。

## 圈空间与边空间

$\mathcal C(G)$是$\mathcal E(G)$的线性子空间。

## 圈空间与基本圈组

给定连通图$G$的一棵生成树，其对应的基本圈组
$$
C_1,C_2,\cdots,C_{\varepsilon-\nu+1}
$$
为$\mathcal C(G)$的一组基，$\mathcal C(G)$的维数为$\varepsilon-\nu+1$。

## 断集空间与边空间

$\mathcal S(G)$是$\mathcal E(G)$的线性子空间。

## 圈向量和断集向量的正交性

任给连通图$G$的圈向量$C\in\mathcal C(G)$和断集向量$S\in\mathcal S(G)$，$C$与$S$的内积$(C,S)=0$。其中的运算是在$F_2$中进行的。

## 基本圈矩阵与基本割集矩阵

给定连通图$G$的生成树$T$，$G$关于$T$的基本圈矩阵与基本割集矩阵分别为
$$
C_f(G)=(I_{\varepsilon-\nu+1}:C_{12}),Sf(G)=(S_{11}:I_{\nu-1}).
$$
其中，$C_{12}$的列对应树$T$的边，$S_{11}$的列对应余树的边，则有
$$
S_{11}=C_{12}^T.
$$

## 邻接矩阵与路径数

设$G=(V,E)$是无向图，$V=\{v_1,v_2,\cdots,v_\nu\}$，其邻接矩阵为$A(G)=(a_{ij})_{\nu\times\nu}$。记$A^n(G)=(a^n_{ij})_{\nu\times\nu}$，则$a^n_{ij}$为图$G$中从$v_i$到$v_j$长为$n$的路径数。

## 关联矩阵与基本关联矩阵的秩

设$G$是连通图，则有
$$
\mathrm{rank}(B(G))=\mathrm{rank}(B_f(G))=\nu-1.
$$

## 生成树与无向图的基本关联矩阵

设$G$是连通图，
$$
e_{i_1}，e_{i_2},\cdots,e_{i_{\nu(G)-1}}\in E(G),
$$
则
$$
G[\{e_{i_1}，e_{i_2},\cdots,e_{i_{\nu(G)-1}}\}]
$$
是$G$的生成树，等价于$B_f(G)$中由第$i_1,i_2,\cdots,i_{\nu(G)-1}$列构成的子矩阵为满秩矩阵。

## 有向图的关联矩阵的行列式的子式

设$B(D)$是有向图$D$的关联矩阵，$B'$是$B(D)$的任意一个子方阵，则有
$$
\det(B')=0或\pm1.
$$

## Binet-Cauchy定理

设$A,B$分别为一个$m\times n$阶与$n\times m$阶矩阵，其中$m\leqslant n$，则$A$与$B$的积的行列式值满足下列公式：
$$
\det(A\times B)=\sum_{1\leqslant k_1<k_2<\cdots<k_m\leqslant n}\det(A(12\cdots m;k_1,k_2,\cdots k_m))\times \det(B(k_1,k_2,\cdots k_m;12\cdots m)).
$$

## 生成树与有向图的基本关联矩阵

设$D$是弱连通有向图，$G$是$D$的底图，
$$
e_{i_1}，e_{i_2},\cdots,e_{i_{\nu(G)-1}}\in E(D),
$$
在略去边
$$
e_{i_1}，e_{i_2},\cdots,e_{i_{\nu(G)-1}}
$$
d 方向后，在底图中则
$$
G[\{e_{i_1}，e_{i_2},\cdots,e_{i_{\nu(G)-1}}\}]
$$
是$G$的生成树，等价于$B_f(D)$中由第$i_1,i_2,\cdots,i_{\nu(G)-1}$列构成的子矩阵为满秩矩阵。

## 生成树个数与基本关联矩阵

设$G$是无环连通无向图，将$G$的每条边任意定向，得到一个有向图$D$。则$G$的生成树个数为
$$
\tau(G)=\det(B_f(D)\times B_f^T(D)).
$$
