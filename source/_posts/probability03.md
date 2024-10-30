---
title: 测度论
tags: 
    - course notes
    - probability
categories:
    - course notes
date: 2024-10-30
mathjax: true
---

## 集类

集合是我们熟悉的概念，但是我们在这部分的内容中还会经常使用到**类**、**空间**和**域**的概念. 这里我暂时不给一个严格的定义，在大致理解这部分内容之后再回来看看. 不过你可以先把类理解成是“更大”的“集合”，而空间是带有一些运算和性质的集合.

我们考虑一个**抽象空间** $\Omega$，在其上定义了并、交、补、差、对称差（$\Delta$）、包含、属于等运算，就像我们常做的那样.

对于$\Omega$的**非空类**$\mathscr{A}$，它可能有一些常见的“封闭性质”：

- 对于补封闭
- 对于交封闭 / 对于并封闭
- 对于差封闭
- 对于有限次交封闭 / 对于有限次并封闭
- 单调且对于可数交封闭 / 对于可数并封闭，i. e.

$$
E_i \in \mathscr{A}, E_i \subset E_{i+1},~\Rightarrow \bigcup_{j=1}^\infty E_i \in \mathscr{A}
$$

$$
E_i \in \mathscr{A}, E_i \supset E_{i+1},~\Rightarrow \bigcap_{j=1}^\infty E_i \in \mathscr{A}
$$

- 对于可数交封闭 / 对于可数并封闭，i. e.

$$
E_i \in \mathscr{A} ~\Rightarrow \bigcup_{j=1}^\infty E_i \in \mathscr{A}
$$

$$
E_i \in \mathscr{A} ~\Rightarrow \bigcap_{j=1}^\infty E_i \in \mathscr{A}
$$

> [!info] $\sigma$ - algebra
> 

由这些封闭条件，我们引入如下定义：

> [!def]
> $\mathscr{F}$是$\Omega$的子集的一个非空类，如果它对补和交（并）封闭，则称其为**域**. 
> 如果单调且对于可数交 / 并封闭，则称其为**单调类**(M. C.). 
> 如果对于补和可数并（交）封闭，则称其为**波莱尔域**(B. F.). （或者说$\sigma$-代数？）

**对于一个域，它是M. C.等价于它是一个B. F. .** 

上述命题反向的证明是显然的（事实上波莱尔域天然是单调类），对于充分性，我们只需要*有限并封闭* + *单调可数并封闭* 可以推出 *可数并封闭* 即可. 事实上这也是显然的，因为$\displaystyle \bigcap_{i = 1}^n E_i \subset \bigcap_{i = 1}^{n + 1} E_i$.

由上述命题我们还可以指出，**如果$\mathscr{F}_0$是一个域，而$\mathscr{F}, ~\mathscr{G}$是包含它的最小单调类与最小波莱尔域，那么两者相等**.

要证明这个命题，我们其实只需要说明类$\mathscr{F}$是一个域就可以了（为什么？），也就是验证他对并和补的封闭性. 

==？==这里没看懂什么个意思，但是有下面的推论：

**如果$\mathscr{F_0}$是一个域，$\mathscr{F}$是包含它的最小波莱尔域，$\mathscr{C}$又使包含$\mathscr{F}_0$的具有单调可数并封闭和单调可数交封闭的集类，则$\mathscr{C}$包含$\mathscr{F}$.

（==推论也没明白是个什么意思，还是问一问吧==）

## 概率测度及其分布函数

### 概率测度

假设$\mathscr{F}$是$\Omega$子集上的一个波莱尔域，那么满足如下条件的，定义在$\mathscr{F}$上的数值集函数（也就是将集合映射到数的函数）就称为概率测度（p. m.）

- $\forall E \in \mathscr{F}, ~\mathscr{P}(E) \geq 0$
- **可数可加性**：如果$\mathscr{F}$中的一列两两不相交的集合${E_i}$，则$\displaystyle \mathscr{P}(\bigcup_i E_i) = \sum_i \mathscr{P}(E_i)$
- $\mathscr{P}(\Omega) = 1$

下面的命题称为**连续性公理**：

$E_n \to \varnothing \Rightarrow \mathscr{P}(E_n) \to 0$

它可以推出单调性. 另外，我们指出：**有限可加性 + 连续性公理等价于可数可加性**.

我们先证明可数可加性蕴含连续性公理（因为蕴含有限可加性是显然的）. 

我们取$E_n \downarrow \varnothing$，则$\displaystyle E_n = \bigcup_{k = n}^\infty(E_k \backslash E_{k+1}) \cap \displaystyle \bigcap_{k = 1}^{\infty} E_k$

> 摆狗钝评：上面的操作就是将一列单调收缩到空集的集合分成了两部分，其中一部分中的集合两两不交，另一部分是原来那一列集合的公共部分（实际是空集）

由可数可加性，我们有（因为公共部分是空集）$$\mathscr{P}(E_n) = \sum_{k = n}^\infty \mathscr{P}(E_k \backslash E_{k+1})$$
因为$E_n \downarrow \varnothing$，所以$\mathscr{P}(E_n)$收敛，而由上式右侧可以知道收敛到0. 这就证明了连续性公理.  ==？==

接下来证明另一个方向. 假设连续性公理和有限可加性成立，我们将得到可数可加性成立.

假设$E_k$两两不交，我们有：

$$
\mathscr{P}(\bigcup_{k=1} E_k) = \mathscr{P}(\bigcup_{k=1}^nE_k) + \mathscr{P}(\bigcup_{k =  n + 1} E_k) = \sum_{k=1}^{n}\mathscr{P}(E_k) + \mathscr{P}(\bigcup_{k =  n + 1} E_k)
$$

所以我们希望证明可数可加性，只需要说明$\displaystyle \bigcup_{k = n+1}E_k \downarrow \varnothing$ 即可. 而这个命题是平凡的，因为对于任意的$x \in E_k$，总有$x \notin E_{k+1}$. 换句话说，对于任意元素，我总能找到足够大的$n$，使得此后集合的病不包含这个元素.

> 此处有一个推论没写

### 样本空间

**样本空间**：我们将三元组$(\Omega, \mathscr{F}, \mathscr{P})$称为一个概率空间.

**迹**：假设$\Delta \subset \Omega$，我们定义$\Delta \cap \mathscr{F} = \\{\Delta \cap F | F \in \mathscr{F}\\}$为$\mathscr{F}$在$\Delta$上的迹，它是$\Delta$的波莱尔域. 我们还可以定义定义在$\Delta \cap \mathscr{F}$ 的集函数（我也真是服了，这里的公式老是渲染不出来）：

$$\mathscr P_\Delta = \displaystyle \frac{\mathscr{P}}{\mathscr{P}_\Delta(E)}$$

 我们称 $(\Delta, \Delta\cap \mathscr{F}, \mathscr P_\Delta)$ 为 $(\Omega, \mathscr{F}, \mathscr{P})$在$\Delta$上的迹.

---

## 例子与问题

这部分以后（也许？）会另外写一篇博客补充.