---
title: Markdown数学公式语法
date: 2020-04-17 12:48:18
tags:
mathjax: true
---

Markdown数学公式繁多，不容易记，此文大致总结一下，以供以后翻阅。
<!--more-->

公式用法：

1. 行内公式：将公式插入到本行中，符号\$公式内容$.
2. 独行公式：将公式插入到新的一行内，并且居中，符号$$公式内容$$。

以下Markdown格式不加\$,加上表示相应公式。

## 上标、下标与组合

|类型|算式|Markdown|
|----|----|--------|
|上标|^|x^4|
|下标|$p_1$|p_1|
|组合|$e^{k-1}$|e^{k-1}|

## 汉字、字体与格式

|类型|算式|Markdown|
|----|----|--------|
|汉字形式|$V_{\mbox{初始}}$|V_{\mbox{初始}}|
|字体控制|$\displaystyle\frac{x+y}{y+z}$|\displaystyle\frac{x+y}{y+z}|
|下划线符号|$\underline{x+y}$|\underline{x+y}|
|标签|$\tag{11}$|\tag{11}|
|上大括号|$\overbrace{a+b+c+d}^{2.0}$|\overbrace{a+b+c+d}^{2.0}|
|下大括号|$a+\underbrace{b+c}_{1.0}+d$|a+\underbrace{b+c}_{1.0}+d|
|上位符号|$\vec{x}\stackrel{\mathrm{def}}{=}{x_1,\dots,x_n}$|\vec{x}\stackrel{\mathrm{def}}{=}{x_1,\dots,x_n}|

## 占位符

|类型|算式|Markdown|
|----|----|--------|
|两个quad空格|$x \qquad y$|x \qquad y|
|quad空格|$x \quad y$|x \quad y|
|大空格|$x \ y$|x \ y|
|中空格|$x \: y$|x \\: y|
|小空格|$x \, y$|x \\, y|
|没有空格|$xy$|xy|
|紧贴|$x\!y$|x\\!y|

## 定界符和组合

|类型|算式|Markdown|
|----|----|--------|
|括号|$（）\big(\big) \Big(\Big) \bigg(\bigg) \Bigg(\Bigg)$|（）\big(\big) \Big(\Big) \bigg(\bigg) \Bigg(\Bigg)|
|中括号|$[x+y]$|[x+y]|
|大括号|$\{x+y\}$|{x+y}|
|自适应括号|$\left(x\right)$，$\left(x{yz}\right)$|\left(x\right)$，$\left(x{yz}\right)|
|组合公式|${n+1 \choose k}={n \choose k}+{n \choose k-1}$|{n+1 \choose k}={n \choose k}+{n \choose k-1}|
|组合公式|$\sum_{k_0,k_1,\ldots>0 \atop k_0+k_1+\cdots=n}A_{k_0}A_{k_1}\cdots$|\sum_{k_0,k_1,\ldots>0 \atop k_0+k_1+\cdots=n}A_{k_0}A_{k_1}\cdots|

## 四则运算

|类型|算式|Markdown|
|----|----|--------|
|加法运算|$x+y=z$|x+y=z|
|减法运算|$x-y=z$|x-y=z|
|加减运算|$x \pm y=z$|x \pm y=z|
|减加运算|$x \mp y=z$|x \mp y=z|
|乘法运算|$x \times y=z$|x \times y=z|
|点乘运算|$x \cdot y=z$|x \cdot y=z|
|星乘运算|$x \ast y=z$|x \ast y=z|
|除法运算|$x \div y=z$|x \div y=z|
|斜除法运算|$x/y=z$|x/y=z|
|分式表示|$\frac{x+y}{y+z}$|\frac{x+y}{y+z}|
|分式表示|${x+y} \over {y+z}$|{x+y} \over {y+z}|

## 高级运算

|类型|算式|Markdown|
|----|----|--------|
|平均数运算|$\overline{xyz}$|\overline{xyz}|
|开二次方运算|$\sqrt x$|\sqrt x|
|开方运算|$\sqrt[3]{x+y}$|\sqrt[3]{x+y}|
|对数运算|$\log(x)$|\log(x)|
|极限运算|$\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$|\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}|
|极限运算|$\displaystyle \lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$|\displaystyle \lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}|
|求和运算|$\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$|\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}|
|求和运算|$\displaystyle \sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$|\displaystyle \sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}|
|积分运算|$\int^{\infty}_{0}{xdx}$|\int^{\infty}_{0}{xdx}|
|积分运算|$\displaystyle \int^{\infty}_{0}{xdx}$|\displaystyle \int^{\infty}_{0}{xdx}|
|微分运算|$\frac{\partial x}{\partial y}$|\frac{\partial x}{\partial y}|
|矩阵表示|$\left[\begin{matrix}a & b & c & d & e\\f & g & h & i & j \\k & l & m & n & o \\p & q & r & s & t\end{matrix} \right]$|\left[\begin{matrix}a & b & c & d & e\\f & g & h & i & j \\k & l & m & n & o \\p & q & r & s & t\end{matrix} \right]|

## 逻辑运算

|类型|算式|Markdown|
|----|----|--------|
|等于运算|$x+y=z$|x+y=z|
|大于运算|$x+y>z$|x+y>z|
|小于运算|$x+y<z$|x+y<z|
|大于等于运算|$x+y \geq z$|x+y \geq z|
|小于等于运算|$x+y \leq z$|x+y \leq z|
|不等于运算|$x+y \neq z$|x+y \neq z|
|不大于等于运算|$x+y \ngeq z$|x+y \ngeq z|
|不大于等于运算|$x+y \not\geq z$|x+y \not\geq z|
|不小于等于运算|$x+y \not\geq z$|x+y \not\geq z|
|不小于等于运算|$x+y \nleq z$|x+y \nleq z|
|约等于运算|$x+y \approx z$|x+y \approx z|
|恒等于运算|$x+y \equiv z$|x+y \equiv z|

## 集合运算

|类型|算式|Markdown|
|----|----|--------|
|属于运算|$x \in y$|x \in y|
|不属于运算|$x \notin y$|x \notin y|
|子集运算|$x \subset y$|x \subset y|
|子集运算|$x \supset y$|x \supset y|
|真子集运算|$x \subseteq y$|x \subseteq y|
|非真子集运算|$x \subsetneq y$|x \subsetneq y|
|真子集运算|$x \supseteq y$|x \supseteq y|
|非真子集运算|$x \supsetneq y$|x \supsetneq y|
|非子集运算|$x \not\subset y$|x \not\subset y|
|非子集运算|$x \not\supset y$|x \not\supset y|
|并集运算|$x \cup y$|x \cup y|
|交集运算|$x \cap y$|x \cap y|
|差集运算|$x \setminus y$|x \setminus y|
|同或运算|$x \bigodot y$|x \bigodot y|
|同与运算|$x \bigotimes y$|x \bigotimes y|
|实数集合|$\mathbb{R}$|\mathbb{R}|
|自然数集合|$\mathbb{Z}$|\mathbb{Z}|
|空集|$\emptyset$|\emptyset|

## 数学符号

|类型|算式|Markdown|
|----|----|--------|
|无穷|$\infty$|\infty|
|虚数|$\imath$|\imath|
|虚数|$\jmath$|\jmath|
|数学符号|$\hat{a}$|\hat{a}|
|数学符号|$\check{a}$|\check{a}|
|数学符号|$\breve{a}$|\breve{a}|
|数学符号|$\tilde{a}$|\tilde{a}|
|数学符号|$\bar{a}$|\bar{a}|
|矢量符号|$\vec{a}$|\vec{a}|
|数学符号|$\acute{a}$|\acute{a}|
|数学符号|$\grave{a}$|\grave{a}|
|数学符号|$\mathring{a}$|\mathring{a}|
|一阶导数符号|$\dot{a}$|\dot{a}|
|二阶导数符号|$\ddot{a}$|\ddot{a}|
|上箭头|$\uparrow$/$\Uparrow$|\uparrow / \Uparrow|
|下箭头|$\downarrow$ / $\Downarrow$|\downarrow / \Downarrow|
|左箭头|$\leftarrow$ / $\Leftarrow$|\leftarrow / \Leftarrow|
|右箭头|$\rightarrow$ / $\Rightarrow$|\rightarrow / \Rightarrow|
|低端对齐省略号|$1,2,\ldots,n$|1,2,\ldots,n|
|中线对齐省略号|$x_1^2 + x_2^2 + \cdots + x_n^2$|x_1^2 + x_2^2 + \cdots + x_n^2|
|竖直对齐省略号|$\vdots$|\vdots|
|斜对齐省略号|$\ddots$|\ddots|

## 希腊字母

|字母|实现|字母|实现|
|----|----|----|----|
|$A$|A|$\alpha$|\alpha|
|$B$|B|$\beta$|\beta|
|$\Gamma$|\Gamma|$\gamma$|\gamma|
|$\Delta$|\Delta|$\delta$|\delta|
|$E$|E|$\epsilon$|\epsilon|
|$Z$|Z|$\zeta$|\zeta|
|$H$|H|$\eta$|\eta|
|$\Theta$|\Theta|$\theta$|\theta|
|$I$|I|$\iota$|\iota|
|$K$|K|$\kappa$|\kappa|
|$\Lambda$|\Lambda|$\lambda$|\lambda|
|$M$|M|$\mu$|\mu|
|$N$|N|$\nu$|\nu|
|$\Xi$|\Xi|$\xi$|\xi|
|$O$|O|$\omicron$|\omicron|
|$\Pi$|\Pi|$\pi$|\pi|
|$P$|P|$\rho$|\rho|
|$\Sigma$|\Sigma|$\sigma$|\sigma|
|$T$|T|$\tau$|\tau|
|$\Upsilon$|\Upsilon|$\upsilon$|\upsilon|
|$\Phi$|\Phi|$\phi$|\phi|
|$X$|X|$\chi$|\chi|
|$\Psi$|\Psi|$\psi$|\psi|
|$\Omega$|\Omega|$\omega$|\omega|