---
title: Graph Theoretic Computer Algorithm
date: 2021-10-25 19:34:01
tags: Graph Theory
categories: Mathematics 
mathjax: true
---

图论算法在计算机科学中扮演着很重要的角色，它提供了对很多问题都有效的一种简单而系统的建模方式。本文简要介绍Dijkstra、Kruskal、Prim、Huffman、交错树、匈牙利、Kuhn-Munkreas、Fleury、逐步插入回路、Edmonds-Johnson、最近邻、最小生成树、最小权匹配、可增载轨道、Ford-Fulkerson最大流、容量有上下界网路的最大流及Warshall算法的操作步骤。

<!--more-->

# Dijkstra算法——最短路径问题

- 输入：加权图$G=(V(G),E(G)),\omega:E(G)\to R^+$，顶点$u_0\in V(G)$。
- 输出：$u_0$到其余所有顶点的距离和最短路径。

1. 任给$u,v\in V(G)$，若$u,v\notin E(G)$，令$\omega(uv)=\infty$；
2. 令$d(u_0)=0,l(u_0)=\$$；任给$u\in V(G)$，$u\in V(G)$，$u\notin u_0$，$d(u)=\infty$，$l(u)=*$；$S_0={u_0}$；$i=0$；
3. 对任给$u\in V(G)-S_i$，若$d(u_i)+\omega(u_iu)\lt d(u)$，则令$d(u)\leftarrow d(u_i)+\omega(u_iu)$，且令$l(u)=u_i$；
4. 选出$u_{i+1}\in V(G)-S_i$，使得$d(u_{i+1})=\min\limits_{u\in V(G)-S_i}d(u)$，令$S_{i+1}=S_i\cup \{u_{i+1}\}$；
5. 若$i=\nu(G)-1$，算法停止；否则，令$i\leftarrow i+1$，转步骤3。

# Kruskal算法——最小生成树问题

- 输入：加权图$G=(V(G),E(G),\omega)$，$\nu=|V(G)|$。
- 输出：$G$的一颗生成树的边子集$\{e_1,e_2,\cdots,e_{\nu-1}\}$。

1. 从$E(G)$中选权最小的边$e_1$；
2. 若已经选定边$e_1,e_2,\cdots,e_i$，则从$E(G)-\{e_1,e_2,\cdots,e_i\}$中选出边$e_{i+1}$使得
   (i)边导出子图$G[\{e_1,e_2,\cdots,e_i,e_{i+1}\}]$不含圈；
   (ii)在满足(i)的条件下，$\omega(e_{i+1})$的权最小，即$\omega(e_{i+1})=\min\limits_{e\in E(G)-\{e_1,e_2,\cdots,e_i\}}\omega(e)$。
3. 反复执行第2步，直到选出$e_{\nu-1}$为止。

# Prim算法——最小生成树问题

- 输入：边权图$G=(V(G),E(G),\omega)$，$\nu=|V(G)|$。
- 输出：$G$的一颗生成树的边子集$E$。

1. 从$V(G)$中任意选取一个顶点$s$，令$V'=\{s\}$，$E'=\emptyset$；
2. 在$(V',\overline{V'})$中选择一条权最小的边$uv$，其中$u\in V'$，$v\in \overline{V'}$令$V'=V'\cup\{u\}$，$E'=E'\cup\{uv\}$；
3. 反复执行第2步，直到$|V'|=\nu$或$|E'|=\nu-1$为止。

# Huffman算法——最优二叉树问题

- 输入：给定实数$w_1\leqslant w_2\leqslant \cdots \leqslant w_t$。
- 输出：带有权值$w_1\leqslant w_2\leqslant \cdots \leqslant w_t$的最优二叉树。

1. 连接以$w_1,w_2$为权的两片树叶，得到带权为$w_1+w_2$的分支点；
2. 在$w_1+w_2,w_3,\cdots.w_t$中再取两个最小的权，连接它们对应的顶点，又得到新的分支点及所带的权。
3. 重复第2步，直到形成一棵树为止。

# 交错树算法——最大匹配问题

- 输入：二分图$G(X,E,Y)$，$G$的匹配$M$，$G$中没有被$M$许配的顶点$u$，不妨设$u\in X$。
- 输出：$G$中关于$M$的$u-$交错树$T_u=(U,E',V')$。

1. $U=\{u\},E'=\emptyset,V=\emptyset$；令$l_{pre}(u)=*$；对$G$中所有的顶点$v\neq u$，令$l_{pre}(v)=NULL$；对$G$中所有的顶点$v$（包括$v$），令$l_{visited}(v)=0$。

2. 若上一步中没有新的顶点加入$U$，算法停止；否则转第3步。

3. 若存在
   $$
   x\in X,l_{pre}(x)\neq NULL,l_{xisited}(x)=0,
   $$
   则对$Y$中所有满足$xy\in E-M$且$l_{pre}(y)=NULL$的顶点$y$，令$$l_{pre}(y)=x;E'\leftarrow E'\cup\{xy\};U\leftarrow U\cup\{x\}$$；最后令$l_{visited}(x)=1$。

4. 若在第3步，在$V$中加入一个新的顶点$y$（同时也将$l_{pre}(y)$从$NULL$修改为$x$），且$y$没有被$M$许配，则已经找到可增广轨道，算法停止；若在第3步没有新的顶点加入$V$，算法停止；否则转到第5步。

5. 若存在
   $$
   y\in Y,l_{pre}(y)\neq NULL,l_{xisited}(y)=0,
   $$
   则对$Y$中所有满足$xy\in M$且$l_{pre}(x)=NULL$的顶点$x$，令$$l_{pre}(x)=y;E'\leftarrow E'\cup\{xy\};U\leftarrow U\cup\{x\}$$；最后令$l_{visited}(y)=1$。转第2步。

# 匈牙利算法——最大匹配问题

- 输入：二分图$G=(X,E,Y)$.
- 输出：$G$的最大匹配$M$。

1. 取$G$的一个初始匹配$M$，比如说$M=\emptyset$。$G' \leftarrow G$。
2. 若$G$为空，或者$G'$中的顶点都被$M$许配，算法停止；否则转第3步。
3. 取$G$中没有被$M$许配的顶点$u$，搜索$u-$交错树$T_u$，若找到可增广轨道，设为$P$，令$M\leftarrow M\oplus E(P)$，转第2步；否则，令$G'\leftarrow G;-V(T)$，转第2步。

# Kuhn-Munkreas算法——最佳匹配问题

- 输入：二分图$G=(X,\Delta,Y),|X|=|Y|$，边权函数$\omega:\Delta\to R$。
- 输出：$G$的最佳匹配$M$。

1. 选取$G$的一个可行顶标$l$，构造相等子图$G_l$。

2. 用匈牙利算法求$G_l$的最大匹配，设为$M$。若$M$是$G_l$的完备匹配，则$M$是$G$的最佳匹配，算法停止；否则，转第3步。

3. 设$u$是$G_l$中未被$M$许配的顶点，不妨设$u\in X$。令
   $$
   Z=\{v|v\in V(G_l),且u,v之间存在交错轨道\},S=X\cap Z,T=Y \cap Z.
   $$
   计算
   $$
   \alpha_l=\min\limits_{x_i\in S,y_i\notin T}\{l(x_i)+l(y_j)-\omega((x_i,y_j))\}.
   $$
   按如下公式修改可行顶标：
   $$
   \hat{l}(v)=l(v)-\alpha_l,v\in S;l(v)+\alpha_l,v\in T;l(v),其它.
   $$
   令$l\leftarrow \hat{l}$，转第1步。

# Fleury算法——Euler回路问题

- 输入：图$G=(V(G),E(G))$。
- 输出：图$G$的一条行迹。

1. 任取$v_0\in V(G)$，令$P_0=v_0$；

2. 假设沿$P_i=v_0e_1v_1e_2\cdots e_iv_i$走到顶点$v_i$，按下面的方法从$E(G)-\{e_1,e_2,\cdots,e_i\}$中选$e_{i+1}$：

   1. $e_{i+1}$与$v_i$关联；

   2. 除非无边可选，否则$e_{i+1}$不选$G_i-\{e_1,e_2,\cdots,e_i\}$的桥。

   若选不到这样的$e_i$，则算法停止。
   
3. 设$v_{i+1}$是$e_{i+1}$关联的另一个顶点，令$$P_{i+1}=v_0e_1v_1e_2\cdots e_iv_ie_{i+1}v_{i+1},i\leftarrow i+1$$​，转2.

# 逐步插入回路算法——Euler回路问题

- 输入：Euler图$G=(V(G),E(G))$。
- 输出：图$G$的一条Euler回路。

1. $$
   i\leftarrow 0,v^*=v_1,v=v_1,P_0=v_1,G_0=G;
   $$

2. 在$G_i$中取与$v$关联的任意一条边$e=vv'$，将$e$及$v'$加入$P_i$中得到$P_{i+1}=P_iev'$；

3. 若$v'=v^*$，转4，否则$i\leftarrow i+1,v\leftarrow v'$，转2；

4. 若$E(P_{i+1})=E(G)$，停止；否则，令$G_{i+1}=G-E(P_{i+1})$，在$G_{i+1}$中任取一条与$P_{o+1}$中某顶点$v_k$关联的边$e$，先将$P_{i+1}$改写成起点（终点）为$v_k$的简单回路，再置$v^*=v_k,v=v_k,i\leftarrow i+1$，转2。

# Edmonds-Johnson算法——中国邮递员问题

- 输入：加权图$G=(V(G),E(G),W(G))$。
- 输出：图$G$的一条最优投递线路。

1. 若$G$中没有奇度顶点，令$G^*=G$，转2，否则求出$G$中度数为奇数的顶点集合$$V_O=\{v|v\in V(G),deg(v)\equiv 1(\mod2) \}$$，转3。
2. 求$G^*$中的Euler回路，停止。
3. 对$V_O$中的每对顶点$u$和$v$，用Dijkstra算法求出其在$G$中的最短距离$dist_G(u,v)$以及最短路径；
4. 以$V_O$为顶点集合构造带权完全图$K_{|V_O|}$，每条边$uv$的权为$dist_G(u,v)$；
5. 求带权完全图$K_{|V_O|}$的总权最小的完备匹配$M$；
6. 针对第5步求得的最小完备匹配中的每条边，给出其两个端点，将该两个端点在$G$中的最短路径上每一条边重复一遍，得到Euler图$G^*$，转2。

# 最近邻法——旅行商问题

- 输入：加权图$G=(V(G),E(G),W(G))$，顶点$v_1$。
- 输出：图$G$的一条Hamilton圈。

1. 从访问$v_1$开始，形成初始轨道$P_1=v_1$；
2. 若已经访问了第$k(k\leqslant \nu-1)$个顶点，形成轨道$P_k=v_1v_2\cdots v_k$，从$V-\{v_1,v_2,\cdots,v_k\}$中选取与$v_k$最近的顶点作为下一步访问的顶点$v_{k+1}$；
3. 当访问完$G$中所有顶点后，形成轨道$P_\nu=v_1v_2\cdots v_\nu$，再回到起点$v_1$得到图$H=v_1v_2\cdots v_\nu v_1$，此即为$G$中的一条Hamilton圈，把它作为旅行商问题的近似解。

# 最小生成树法——旅行商问题

- 输入：加权图$G=(V(G),E(G),W(G))$。
- 输出：图$G$的一条Hamilton圈。

1. 求$G$的一棵最小生成树$T$；
2. 将$T$中各边都添加一条平行边，平行边的权与其对应边的权相同。设所得图为$G^*$，则$G^*$为Euler图；
3. 从某顶点$v$出发，求$G$中一条Euler回路$C_v$；
4. 在$G$中按下面的方法求从顶点$v$出发的Hamilton圈。从点$v$出发沿$C_v$“抄近路”访问$G$的各顶点，即：假定当前访问过的顶点为$x$，$C_v$上$x$的后续两个顶点分别为$v$与$w$，若$y$在此之前已经被访问，则直接从$x$经过边$xw$访问$w$，直到访问完所有顶点为止。最后走出一条$G$的一条Hamilton圈$H_\nu$，就是$G$的最优解的近似解。

# 最小权匹配法——旅行商问题

- 输入：加权图$G=(V(G),E(G),W(G))$，顶点$v_1$。
- 输出：图$G$的一条Hamilton圈。

1. 求$G$的一棵最小生成树$T$；
2. 设$T$中度为奇数的顶点集合为$V_O=\{v_1,v_2,\cdots,v_{2k}\}$，求$V_O$的导出子图$G[V_O]=K_{2k}$中总权最小的完备匹配$M$，将$M$中的$k$条边加到$T$上，得到Euler图$G^*$;
3. 在$G^*$中求从某顶点$v$出发的一条Euler回路$C_v$；
4. 在$G$中，从$v$出发，沿$C_v$中的边按“抄近路法”走出Hamilton圈$H_\nu$。

# 可增载轨道算法——最大流问题

- 输入：网络$N=(D,s,t,c)$，流函数$f$。
- 输出：一条可增载轨道，或指出当前流函数是最大流。

1. $S=\{s\}$，令$prev(s)=*$。
2. 若$t\in S$，则已经找到可增载轨道，通过$prev(t)$回溯输出可增载轨道，算法停止；否则，转第3步。
3. 若存在$u\in S$，$v\in\overline S$，使得$(u,v)\in E(D)$且边$(u,v)$未满载，即$f((u,v))<c((u,v))$（$(u,v)$是正向边），则令$S\leftarrow S\cup\{v\},prev(v)=u$，转第2步；否则，转第4步。
4. 若存在$u\in S，v\in\overline S$，使得$(u,v)\in E(D)$且边$(u,v)$正载，即$f((u,v))》c((u,v))$（$(u,v)$是反向边），则令$S\leftarrow S\cup\{v\},prev(v)=u$，转第2步；否则，输出无可增载轨道，算法停止。

# Ford-Fulkerson最大流算法——最大流问题

- 输入：网络$N=(D,s,t,c)$。
- 输出：最大流函数$f$。

1. 取初始流函数$f$。

2. 调用可增载轨道算法。若找到可增载轨道$P(s,t)$，则构造新的流函数$\overline f$如下：
   $$
   \overline f(e)=f(e)+l(P),e是正向边;f(e)-l(P),e是反向边;f(e)，其它.
   $$
   令$f\leftarrow\overline f$，转第2步。否则，没有找到可增载轨道，输出$f$是最大流。停止。

# 容量有上下界网路的最大流算法——最大流问题

- 输入：容量有上下界网络$N=(D,s,t,b,c)$。
- 输出：最大流函数$f$，或断定$N$没有可行流。

1. 构造$N$的伴随网络$N'=(D',s',t',c')$。
2. 用2F算法求出$N'$的最大流函数$f'$。
3. 若$f'$满足，任给$v\in V(D)$，$f'$使得边$(s',v)$满载，即$f'((s',v))=c'((s',v))$，则转第4步；否则，输出结论“$N$没有可行流”，算法停止。
4. 根据$f'$，构造$N$的一个可行流$f$：任给$e\in E(D)$，$f(e)=f'(e)+b(e)$；
5. 以$f$作为初始流函数，用2F算法求出$N$的最大流，算法停止。

# Warshall算法——邻接矩阵问题

- 输入：有向图$D$的邻接矩阵$A(D)=(a_{ij})_{\nu\times\nu}$。
- 输出：可达性矩阵$R(D)=(r_{ij})_{\nu\times\nu}$。若$v_i$在$G$中可达$v_j$，则$r_{ij}=1$；否则$r_{ij}=0$。

1. 对所有$1\leqslant i,j\leqslant\nu$，若$a_{ij}>0$，令$r_{ij}^0=1$；否则$a_{ij}=0$，令$r_{ij}^0=0$；令$l=0$；

2. 若$l=\nu$，输出
   $$
   R(D)=(r_{ij})_{\nu\times\nu}=(r_{ij}^\nu)_{\nu\times\nu,}
   $$
   算法停止；否则转第3步。

3. 对所有的$1\leqslant i\leqslant\nu$，若$r_{i(l+1)}^l=1$，则对所有的$1\leqslant j\leqslant\nu$，令$r_{ij}^{l+1}=r_{ij}^l\vee r_{(l+1)j}^l$；否则令$r_{ij}^{l+1}=r_{ij}^l$。转第4步。

4. 令$l\leftarrow l+1$，转第2步。

