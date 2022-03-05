---
title: Solutions to Hard Problems of Mathematical Analysis
date: 2021-10-23 17:31:06
tags: Mathematical Analysis 
categories: Mathematics 
mathjax: true
---

# 中国科学技术大学2019-2020学年数学分析(B2)测试真题难题集萃

  题解来源：5，13，14：叶升宇；11，15：陈景毅；12：刘枭男；9：陈卿（教授）。

<!--more-->


由$\LaTeX$生成的PDF版本链接：[Solutions to Hard Problems of Mathematical Analysis](https://gsxgoldenlegendary.github.io/files/math01.pdf)

## 向量场的微商

1.设$$\boldsymbol{v}=a\boldsymbol{i}+b\boldsymbol{j}+c\boldsymbol{k}$$是常向量，$$\boldsymbol{r}=x\boldsymbol{i}+y\boldsymbol{j}+z\boldsymbol{k}$$.求向量场$$\boldsymbol{v}\times\boldsymbol{r}$$的旋度。

解：
	利用向量外积公式$$\nabla\times(\boldsymbol{v}\times\boldsymbol{r})=-(\nabla\cdot\boldsymbol{v})\boldsymbol{r}+(\nabla\cdot\boldsymbol{r})\boldsymbol{v}=(\nabla\cdot\boldsymbol{r})\boldsymbol{v}=3\boldsymbol{v}.$$

## 二重积分

2.求积分$$\int_0^{\frac{\pi}{6}}dy\int_y^\frac{\pi}{6}\frac{\cos x}{x}dx.$$

解：
	$$\int_0^{\frac{\pi}{6}}dy\int_y^\frac{\pi}{6}\frac{\cos x}{x}dx=\int_0^{\frac{\pi}{6}}dx\int_0^x\frac{\cos x}{x}dy=\int_0^\frac{\pi}{6}\cos xdx=\frac{1}{2}.$$

## 二重积分的换元

3.设$$D=\{(u.v)|u\geqslant 0,v\geqslant 0\}$$为无界区域。求$$\iint_D e^{-u^2-v^2-2uv\cos \alpha}dudv,  $$其中$$\alpha \in (0,\frac{\pi}{2})$$为常数。

解：
    做代换$$t=u-v\cos\alpha,s=v\sin \alpha,$$
    则参数范围$$D'=\{(t,s)|0\leqslant t,0\leqslant s\},$$
    代换的Jacobi行列式$$\frac{\partial(u,v)}{\partial(t,s)}=\frac{1}{\sin\alpha}.$$
    原式变为$$\iint_{D^{'}} e^{-s^2-t^2}|\frac{1}{\sin\alpha}|dtds .$$
    利用常用积分$$\int_{0}^{+\infty} \int_{0}^{+\infty} e^{-x^2-y^2}dxdy=\frac{\sqrt{\pi}}{2}, $$
    得原积分为$$\frac{\sqrt{\pi}}{2\sin\alpha}.$$

## 数量场在曲面上的积分

4.设曲面$$S=\{(x,y,z)\in\mathbb{R}^2|x+y+z=1,x,y,z\geqslant0\}.$$求$$\iint_SxyzdS.$$

解：
	使用$x,y$做参数，则对应的面积元$$dS=\sqrt{1+z_x^{'2}+z_y^{'2}}dxdy=\sqrt{3}dxdy ,$$
	参数范围$$D=\{(x,y)|x,y\geqslant 0,x+y\leqslant 1\}.$$
	原式变为$$\iint_Dxy(1-x-y)\sqrt{3}dxdy=\sqrt{3}\int_{0}^{1}dx \int_{0}^{1-x}(xy-x^2y-xy^2)dy=\sqrt{3}\int_{0}^{1}(\frac{x(1-x)^2}{2}-\frac{x^2(1-x)^2}{2}-\frac{x(1-x)^3}{3})dx=\frac{\sqrt{3}}{120}.$$

5.求曲面$(x^2+y^2+z^2)^2=2xy(x,y\geqslant 0)$的面积。

解：
	换为球坐标,则参数曲面方程$$\boldsymbol{r}=p\sin\theta\cos\phi\boldsymbol{i}+p\sin\theta\sin\phi\boldsymbol{j}+p\cos\theta\boldsymbol{k}$$
	其中$$p=\sin\theta \sqrt{\sin 2\phi},0\leqslant \phi\leqslant \frac{\pi}{2},0\leqslant \theta \leqslant\pi,$$$$p_\theta^{'}=\cos\theta\sqrt{\sin2\phi},p_\phi^{'}=\frac{\sin\theta\cos2\phi}{\sqrt{\sin2\phi}}.$$
	记$$E=\boldsymbol{r}_\theta^{'2}=\cos^2\phi(p\cos\theta+p_\theta^{'}\sin\theta)^2+\sin^2\phi(p\cos\theta+p_\theta^{'}\sin\theta)^2+(-p\sin\theta+p_\theta^{'}\cos\theta)^2=p^2+p_\theta^{'2};$$$$G=\boldsymbol{r}_\phi^{'2}=\sin^2\theta(p_\phi^{'}\cos\phi-p\sin\phi)^2+\sin^2\theta(p_\phi^{'}\sin\phi+p\cos\phi)^2+\cos^2\theta p_\phi^{'2}=p^2\sin^2\theta+p_\phi^{'2};$$$$F=\boldsymbol{r}_\theta^{'}\cdot\boldsymbol{r}_\phi^{'}=\cos\phi(p\cos\theta+p_\theta^{'}\sin\theta)\sin\theta(p_\phi^{'}\cos\phi-p\sin\phi)+\sin\phi(p\cos\theta+p_\theta^{'}\sin\theta)\sin\theta(p_\phi^{'}\sin\phi+p\cos\phi)+(-p\sin\theta+p_\theta^{'}\cos\theta)\cos\theta p_\phi^{'}=p_\theta^{'}p_\phi^{'}.$$
	则面积元$$dS=|\boldsymbol{r}_\theta^{'2}\times\boldsymbol{r}_\phi^{'2}|d\theta d\phi=\sqrt{EG-F^2}d\theta d\phi,=\sqrt{(p^2+p_\theta^{'2})(p^2\sin^2\theta+p_\phi^{'2})-p_\theta^{'2}p_\phi^{'2}}d\theta d\phi=\sqrt{(\sin^2\theta \sin 2\phi+\cos^2\theta\sin2\phi)(\sin^2\theta \sin 2\phi\sin^2\theta+\frac{\sin^2\theta\cos^22\phi}{\sin2\phi})-\cos^2\theta\sin2\phi\frac{\sin^2\theta\cos^22\phi}{\sin2\phi}}d\theta d\phi=\sin^2\theta d\theta d\phi.$$
	曲面面积$$\iint_Sds=\int_0^{\frac{\pi}{2}}d\phi\int_0^\pi\sin^2\theta d\theta=\frac{\pi^2}{4}.$$

## 向量场在曲线上的积分

6.设$$f\in C^1(\mathbb{R}^2),$$满足$$|\nabla f|^2=(\frac{\partial f}{\partial x})^2+(\frac{\partial f}{\partial y})^2\equiv 1.$$
（1）证明：$$\forall \boldsymbol{P},\boldsymbol{Q} \in \mathbb{R}^2,|f(\boldsymbol{Q})-f(\boldsymbol{P})|\leqslant|\boldsymbol{P}-\boldsymbol{Q}|;$$
（2）设光滑曲线$\boldsymbol{r}(t)=x(t)\boldsymbol{i}+y(t)\boldsymbol{j}(t\in[a,b])$满足$$\frac{d\boldsymbol{r}}{dt}=\nabla f(\boldsymbol{r}(t))=\frac{\partial f}{\partial x}(x(t),y(t))\boldsymbol{i}+\frac{\partial f}{\partial y}(x(t),y(t))\boldsymbol{j},$$
证明：$\boldsymbol{r}(t)$是直线段。

解：
	记$$\boldsymbol{P}=(x_1,y_1),\boldsymbol{Q}=(x_2,y_2).$$
	由微分中值定理,存在$$x',y'$$有$$|f(\boldsymbol{Q})-f(\boldsymbol{P})|=|(x_2-x_1)\frac{\partial f}{\partial x}(x',y')+(y_2-y_1)\frac{\partial f}{\partial y}(x',y')|$$
	由柯西不等式$$\leqslant \sqrt{(x_2-x_1)^2+(y_2-y_1)^2}\sqrt{(\frac{\partial f}{\partial x})^2+(\frac{\partial f}{\partial y})^2}$$
	由已知$$=\sqrt{(x_2-x_1)^2+(y_2-y_1)^2}$$$$=|\boldsymbol{P}-\boldsymbol{Q}|.$$
	取$$\boldsymbol{P}=\boldsymbol{r}(a),\boldsymbol{Q}=\boldsymbol{r}(b),$$

则$$\int_r |dr|=\int_a^b |\nabla f|dt=\int_a^b dt=\int_a^b \nabla f\cdot \nabla fdt=\int_r \nabla f\cdot d\boldsymbol{r}=\int_{\boldsymbol{P}}^{\boldsymbol{Q}}df=|f(\boldsymbol{Q})-f(\boldsymbol{P})|\leqslant|\boldsymbol{P}-\boldsymbol{Q}|.$$
	其中$$\int_r |dr|$$为$\boldsymbol{P},\boldsymbol{Q}$两点间的曲线长度，$|\boldsymbol{P}-\boldsymbol{Q}|$为$\boldsymbol{P},\boldsymbol{Q}$两点间的直线长度，表明两点间曲线长度不大于直线长度，只能说明该曲线是直线。

7.设D是平面有界区域，$L=\partial D$是光滑曲线，$\boldsymbol{n}$是$\partial D$的单位外法向量，$\boldsymbol{v}\in C_1(D),\boldsymbol{v}=P\boldsymbol{i}+Q\boldsymbol{j}.$
用Green公式证明：$$\int_L(\boldsymbol{v}\cdot\boldsymbol{n})ds=\iint_D(\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y})dxdy.$$

解：
	设单位外法向量$$\boldsymbol{n}=\cos \alpha \boldsymbol{i}+\cos \beta \boldsymbol{j},$$
	则逆时针单位切向量$$\boldsymbol{\tau}=-\cos\beta\boldsymbol{i}+\cos\alpha\boldsymbol{j}.$$
	一方面$$\boldsymbol{\tau}ds=-\cos\beta\boldsymbol{i}ds+\cos\alpha\boldsymbol{j}ds ,$$
	另一方面$$\boldsymbol{\tau}ds=\boldsymbol{i}dx+\boldsymbol{j}dy$$
	故$$dx=-\cos\beta ds ,\,dy=cos\alpha ds.$$
	回到原式$$\int_L(\boldsymbol{v}\cdot\boldsymbol{n})ds=\int_L(P\cos\alpha ds+Q\cos\beta ds)$$
	利用Green公式$$=\int_LPdy-Qdx=\iint_D(\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y})dxdy.$$

## 向量场在曲面上的积分

8.设曲面$$S=\{(x,y,z)|x^2+y^2+z^2=1,z\geqslant0\},$$定向与z轴正向同侧。
设$$f=\frac{1+z}{1+x^2+y^2},g=xy+yz+zx.$$求积分$$\iint_S(\nabla f\times\nabla g)\cdot d\boldsymbol{S}.$$

解：
	取曲面$$S'=\{(x,y,z)|x^2+y^2\leqslant1,z=0\},$$
	定向与Z轴反向，则S与S'构成封闭曲面，定向向外。设其围城的区域为V。
	由Gauss定理$$\iint_{S+S'}(\nabla f\times\nabla g)\cdot  d\boldsymbol{S}=\iiint_V\nabla\cdot(\nabla f\times\nabla g) dV= \iiint_V(\nabla f\cdot\nabla\times\nabla g)-\nabla g\cdot\nabla\times\nabla f)\,dV=0.$$
	$$\iint_{S'}(\nabla f\times\nabla g)\cdot  d\boldsymbol{S}=\iint_{S'}(\frac{-2x}{(1+x^2+y^2)^2},\frac{-2y}{(1+x^2+y^2)^2},\frac{1}{1+x^2+y^2})\times(y,x,x+y)\cdot d\boldsymbol{S}=\iint_{S'}\frac{2y^2-2x^2}{(1+x^2+y^2)^2} dx dy=\int_0^{2\pi}-\cos 2\theta d\theta\int_0^1\frac{r^2}{(1+r^2)^2} dr^2=0.$$
	故$$\iint_S(\nabla f\times\nabla g)\cdot  d\boldsymbol{S}=(\iint_{S+S'}-\iint_{S'})(\nabla f\times\nabla g)\cdot d\boldsymbol{S}=0.$$

9.设$\Omega$是$\mathbb{R}^3$的有界区域，$\partial \Omega$是光滑曲面。

（1）设$$f,g\in C^2(\overline{\Omega}),$$满足

$$\Delta f=\Delta g,f|_{\partial \Omega} =g|_{\partial \Omega}$$
证明：$$f=g.$$
	（2）设$\boldsymbol{v}_1,\boldsymbol{v}_2$是定义在$\overline{\Omega}$上的光滑向量场（二阶偏导数连续），满足
$$\nabla\times\boldsymbol{v}_1=\nabla\times\boldsymbol{v}_2$$
$$\nabla\cdot\boldsymbol{v}_1=\nabla\cdot\boldsymbol{v}_2$$
$$\boldsymbol{v}_1|_{\partial\Omega}=\boldsymbol{v}_2|_{\partial\Omega}$$
证明：
$$\boldsymbol{v}_1=\boldsymbol{v}_2$$

 解：
 	记$$h=f-g,$$
 	则
$$\Delta h=0,h|_{\partial \Omega}=0,$$
要证$$h=0.$$
利用Gauss定理
$$0=\iint_{\partial\Omega}h\nabla h\cdot\,d\boldsymbol{S} =\iiint_\Omega\nabla\cdot(h\nabla h)\,dV=  \iiint_\Omega((\nabla h)^2+h\Delta h)\,dV=\iiint_\Omega(\nabla h)^2\,dV.$$
故$$\nabla h=\boldsymbol{0}.$$
这样$h$为常数，又
$$h|_{\partial D}=0$$

 得$h=0$。
 	设$$\boldsymbol{u}=\boldsymbol{v}_1-\boldsymbol{v}_2=(P,Q,R),$$
 则

$$\nabla\times\boldsymbol{u}=\boldsymbol{0},\nabla\cdot\boldsymbol{u}=0,\boldsymbol{u}|_{\partial \Omega}=0.$$

即$$\frac{\partial Q}{\partial z}=\frac{\partial R}{\partial y},\frac{\partial R}{\partial x}=\frac{\partial P}{\partial z},\frac{\partial P}{\partial y}=\frac{\partial Q}{\partial x},\frac{\partial P}{\partial x}+\frac{\partial Q}{\partial y}+\frac{\partial R}{\partial z}=0.$$
求导得$$\frac{\partial^2 R}{\partial xz}=\frac{\partial^2 P}{\partial z^2},\frac{\partial^2 P}{\partial y^2}=\frac{\partial^2 Q}{\partial xy},\frac{\partial^2 P}{\partial x^2}+\frac{\partial^2 Q}{\partial xy}+\frac{\partial^2 R}{\partial xz}=0.$$
得到$$\Delta P=0.$$
由（1）知$$P=0.$$
同理$$Q=0,R=0,$$
即$$\boldsymbol{u}=(0,0,0)=\boldsymbol{0}.$$

## 函数的Fourier级数

10.求函数$$y=|x|,x\in[-\pi,\pi]$$的Fourier级数。

解：
	$$a_0=\frac{2}{\pi}\int_0^{\pi}xdx=\pi,$$$$a_n=\frac{2}{\pi}\int_0^{\pi}x\cos nxdx=\frac{\cos n\pi-1}{n^2\pi}.$$$$y\sim \frac{\pi}{2}+\frac{2}{\pi}\sum_{n = 0}^{\infty}\frac{(\cos n\pi-1)\cos nx}{n^2}=\frac{\pi}{2}-\frac{4}{\pi}\sum_{n=1}^\infty \frac{\cos ((2n+1)x)}{(2n+1)^2},x\in[-\pi,\pi] $$

11.求和：$$\frac{4}{\pi}\sum_{n=0}^\infty\frac{\sin ((2n+1)x)}{(2n+1)^3},x\in[-\pi,\pi]$$

解：
	因为$f(x)$在$[-\pi,\pi]$上连续且$f(-\pi)=f(\pi)$，故由Dirichlet定理，$$\frac{\pi}{2}+\frac{4}{\pi}\sum_{n=1}^\infty \frac{\cos ((2n+1)x)}{(2n+1)^2}$$在$[-\pi,\pi]$上一致收敛，
	且有$$\frac{\pi}{2}-\frac{4}{\pi}\sum_{n=1}^\infty \frac{\cos ((2n+1)x)}{(2n+1)^2}=x.$$
	在$[0,\pi)$上两边积分$$\frac{\pi}{2}x-\frac{4}{\pi}\sum_{n=1}^\infty \frac{\sin ((2n+1)x)}{(2n+1)^3}=\frac{x^2}{2}+C.$$
	取$x=0$得$C=0$。
	由原式是奇函数，故

$$\frac{4}{\pi}\sum_{n=0}^\infty\frac{\sin ((2n+1)x)}{(2n+1)^3}=\begin{aligned}\frac{\pi}{2}-\frac{x^2}{2},x\in[-\pi,0];\frac{\pi}{2}+\frac{x^2}{2}.\in(0,-\pi].\end{aligned}$$

12.设$\{b_n\}$ 是单调下降且非负数列，且级数 $$\sum_{n=1}^\infty b_n\sin nx$$在$[-\pi,\pi]$一致收敛。证明：$$\lim_{n\to \infty}nb_n=0.$$

解：
	由Cauchy收敛准则，对$\forall \epsilon>0,\exists N,$当n，m>N时（不妨设n>m），对$\forall x$,
	总有$$|b_m\sin mx+\cdots +b_n\sin nx|<\epsilon.$$
	取$x=\frac{\pi}{4m},n=2m-1$,
	则利用$b_n$的单调递减性有$$mb_{2m}\sin \frac{\pi}{4}<b_m \sin \frac{\pi}{4}+\cdots +b_{2m-1}\sin \frac{2m-1}{4m}\pi<\epsilon.$$
	得到对$\forall \epsilon>0$，都存在N使得对$\forall 2m>2N$,$2mb_{2m}<\frac{\epsilon}{\sqrt{2}}$，
	即$$\lim_{n\to \infty}nb_n=0.$$

## 含参变量的反常积分

13.设$$F(t)=\int_0^{+\infty}\frac{\sin tx}{1+x^2}\,dx.$$求证：
（1）$F(t)$在$(0,+\infty)$上连续；
（2）$F(t)$在$(0,+\infty)$上可导；
（3）$F(t)$在$(0,+\infty)$上二阶可导且满足方程$F^{''}(t)-F(t)=-\frac{1}{t}$。

解：
	因为$$|\int_0^{+\infty}\frac{\sin tx}{1+x^2}dx|<\int_0^{+\infty}\frac{1}{1+x^2}dx=\frac{\pi}{2},$$
	由Weierstrass判别法知$$\int_0^{+\infty}\frac{\sin tx}{1+x^2}dx$$关于t一致收敛，故$F(t)$连续。
	对于$$\int_0^{+\infty}\frac{x\cos tx}{1+x^2}dx,$$$x=0$不是瑕点，所以只需考虑$$\int_1^{+\infty}\frac{x\cos tx}{1+x^2}dx$$关于t在t>0上的一致收敛性即可。
	由于$$|\int_0^{+\infty}\cos txdx|<\frac{2}{t}\leqslant2,$$
	对每个固定的t，$$\frac{x}{1+x^2}$$是x的单调函数，且关于t一致趋于0，由Dirichlet判别法知$$\int_1^{+\infty}\frac{x\cos tx}{1+x^2}dx$$一致收敛。
	又$$\int_0^{+\infty}\frac{\sin tx}{1+x^2}dx$$收敛，$$\frac{\sin tx}{1+x^2},\frac{x\cos tx}{1+x^2}$$在$(0,+\infty)\times(0,+\infty)$上连续，所以$F(t)$可导，且有$$F^{'}(t)=\int_0^{+\infty}\frac{x\cos tx}{1+x^2}dx=\frac{1}{t}\int_0^{+\infty}\frac{x}{1+x^2}d(\sin tx)=\frac{1}{t}\frac{x\sin tx}{1+x^2}|_0^{+\infty}-\frac{1}{t}\int_0^{+\infty}\sin txd(\frac{x}{1+x^2})=\frac{1}{t}\int_0^{+\infty}\frac{x^2-1}{(1+x^2)^2}\sin txdx=\frac{F(t)}{t}-\frac{2}{t}\int_0^{+\infty}\frac{\sin tx}{(1+x^2)^2}dx.$$
	即$$tF^{'}(t)=F(t)-2\int_0^{+\infty}\frac{\sin tx}{(1+x^2)^2}dx,$$
	由于$$|\int_0^{+\infty}\sin tx\,dx|<\frac{2}{t},$$$$\frac{1}{(1+x^2)^2}$$单调趋于0，由Dirichlet判别法知$$\int_1^{+\infty}\frac{\sin tx}{(1+x^2)^2}dx$$收敛。
	对于$$\int_0^{+\infty}\frac{x\cos tx}{(1+x^2)^2}dx,$$$x=0$不是瑕点，所以只需考虑$$\int_1^{+\infty}\frac{x\cos tx}{(1+x^2)^2}dx$$关于t在$t>0$上的一致收敛性即可。
	由于$$|\int_0^{+\infty}\cos tx\,dx|<\frac{2}{t}\leqslant2,$$对每个固定的t，$$\frac{x}{(1+x^2)^2}$$是x的单调函数，且关于t一致趋于0，由Dirichlet判别法知$$\int_1^{+\infty}\frac{x\cos tx}{(1+x^2)^2}dx$$一致收敛。
	又$$\frac{\sin tx}{(1+x^2)^2},\frac{x\cos tx}{(1+x^2)^2}$$在$(0,+\infty)\times(0,+\infty)$上连续，所以$F(t)$可导。
	两边求导得$$tF^{''}(t)+F^{'}(t)=F^{'}(t)-2\int_0^{+\infty}\frac{x\cos tx}{(1+x^2)^2}dx=F^{'}(t)+\int_0^{+\infty}\cos txd(\frac{1}{1+x^2})$$$$=F^{'}(t)+\cos tx\frac{1}{1+x^2}|_0^{+\infty}+t\int_0^{+\infty}\frac{\sin tx}{1+x^2}\,dx=-1+tF(t).$$即$$tF^{''}(t)=-1+tF(t),$$得$$F^{''}(t)-F(t)=-\frac{1}{t}.$$

14.设$|\alpha|\neq 1$，证明积分$$\int_0^{+\infty}\frac{\sin x\sin \alpha x}{x}dx$$收敛，并求其值。

解：
	由于$x=0$是可去瑕点，故只需将原积分视为无穷积分。
	注意到$$|\int_a^b\sin x\sin \alpha x| dx=\frac{1}{2}|\int_a^b\cos (1-\alpha)x-\cos (1+\alpha)x|\leqslant|\frac{1}{1-\alpha}|+|\frac{1}{1+\alpha}|,$$
	又$\frac{1}{x}$单调趋于0，由Dirichlet判别法知原积分收敛。
	引入积分因子，并记$$I(\beta)=\int_0^{+\infty}e^{-\beta x}\frac{\sin x\sin \alpha x}{x}dx.$$
    在$\beta>\beta_0>0$时，$$|I(\beta)|<|\int_0^{+\infty}e^{-\beta x}{x}dx |,$$
    而$$\int_a^b e^{-\beta x}dx $$一致有界。
    对固定的$\beta$, $$\frac{1}{x} $$单调一致趋于0。
    由Dirlichlet判别法知$$\int_0^{+\infty}e^{-\beta x}{x}dx$$一致收敛。
    由比较判别法知$I(\beta)$收敛。
    由于$$|\int_0^{+\infty}-e^{-\beta x}\sin x\sin \alpha x\,dx|<\int_0^{+\infty}e^{-\beta x}dx =1,$$
    故由比较判别法知$$\int_0^{+\infty}-e^{-\beta x}\sin x\sin \alpha xdx$$一致收敛。
    又由$$e^{-\beta x}\frac{\sin x\sin \alpha x}{x},-e^{-\beta x}\sin x\sin \alpha x$$ 在$(0,+\infty)\times(\beta_0,+\infty)$上连续，
    故$I(\beta)$可导，且有$$I^{'}(\beta)=\int_0^{+\infty}-e^{-\beta x}\sin x\sin \alpha xdx=-\frac{1}{2}\int_0^{+\infty}e^{-\beta x}(\cos(1-\alpha )x-\cos(1+\alpha)x)dx=-\frac{1}{2}\frac{\beta}{\beta^2+(\alpha-1)^2}+\frac{1}{2}\frac{\beta}{\beta^2+(\alpha+1)^2}.$$
    积分得$$I(\beta)=\frac{1}{4}\ln \frac{(\alpha +1)^2+\beta^2}{(\alpha -1)^2+\beta^2}+C.$$当$\beta\to\infty$时，$I(\beta)\to C$。
    另一方面由$$\int_0^{+\infty}e^{-\beta x}\frac{\sin x\sin \alpha x}{x}dx$$的连续性知$I(\beta)\to0,$
    故$C=0$。
    这样$$\int_0^{+\infty}\frac{\sin x\sin \alpha x}{x}dx=I(\beta)|_{\beta=0}=\frac{1}{2}\ln \frac{|\alpha+1|}{|\alpha-1|}.$$

## Euler积分

15.计算无穷积分$$I=\int_1^{+\infty}t^2e^{t(2-t)}dt.$$

解：
	$$I=\int_1^{+\infty}t^2e^{t(2-t)}dt=\int_0^{+\infty}(1+s)^2e^{1-s^2}ds=e\int_0^{+\infty}e^{-s^2}ds+e\int_0^{+\infty}e^{-s^2}ds^2+\frac{e}{2}\Gamma(\frac{1}{2})=e+\frac{3\sqrt{\pi}e}{4}.$$

