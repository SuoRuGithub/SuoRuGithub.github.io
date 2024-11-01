---
title: 主定理
tags: 
    - course notes
    - data structure
categories:
    - course notes
date: 2024-09-17
mathjax: true
---

故事要从一道题说起[^2]：

![故事的开始](/images/hw1-master-thm.png)

在解决这个问题之前，我们恐怕需要先了解一下什么是主定理.

## 问题的定义

上面我们分析了若干个程序的时间复杂度，不难发现，有递归的程序的复杂度不是那么容易分析. 

形式化地讲，递归的函数会形如：

$$
T(n) = aT(n/b) + f(n)
$$

在上面的式子中，$n$表示我们问题的规模. 我们希望知道一个函数$T$在此规模下的时间复杂度. 而这个函数会递归地将这个问题拆分成$a$个同样需要函数$T$解决的子问题，其中每个子问题的规模是$n/b$，而且在这个拆分的过程中会额外需要一些步骤，它们的成本记作$f(n)$.

## 从特殊情况讨论

为了说明这个问题，我们先考虑一种简单的情况，抹掉$f(n)$，计算下面这个东西的复杂度：

$$
\begin{equation}
T(n) = aT(n/b) \tag{1}
\end{equation}
$$

首先思考，*上面这个递归会进行多少层？*

递归的核心思路就是：*你希望解决一个大问题是吗？那就先解决一个小问题吧！* 当问题已经被分解至答案显而易见时，递归就可以退出了. 形式化地讲，每次递归，我们都会将$n$规模的问题转化成$n/b$规模的小问题，当规模达到$1$（即常数），递归就可以结束了. 所以我们可以将$(1)$式展开为：

$$
\displaystyle 
\begin{matrix} 
     & k \\\\
    T(n)= & \overbrace{a(a(a\cdots a(T(\frac{n}{b^k})\cdots)))} \\
\end{matrix}
$$

其中$k=\log_bn$，因为$n/b^k=1$. 而且$\displaystyle T(\frac{n}{b^k})$也应该是一个常数时间可以解决的问题，所以总的时间复杂度为：

$$
\displaystyle a^{\log_b n} = n^{\log_b a}
$$

*为什么要变换形式呢？第一个不伦不类，换成n这样多项式的形式就顺眼多了*

这样看来，对于形如$(1)$式这样的递归问题，其复杂度应当是多项式的，而且**阶**为$\displaystyle \log_b a$.

## 主定理

递归将大问题拆成小问题，**but at what cost?** 拆分问题是有代价的——为了拆分问题我们需要$f(n)$.那么$f(n)$会如何影响最终的复杂度呢？

这就引入了主定理，主定理的内容如下[^1]：

$\displaystyle f(n) = \Theta(n^{\log_b a} log^{\epsilon}n)$


{% notel yellow 主定理 %}
**case1**
如果存在$\epsilon >0$，使得
$$\displaystyle f(n) = O(n^{\log_b (a) - \epsilon})$$
那么
$$\displaystyle T(n) = \Theta(n^{\log_b a})$$
**case2**
如果存在$\epsilon \geq0$，使得
$$\displaystyle f(n) = \Theta(n^{\log_b a} log^{\epsilon}n)$$
那么
$$\displaystyle T(n) = \Theta(n^{\log_b a}log^{\epsilon+1}n)$$
**case3**
如果存在$\epsilon >0$，使得
$$\displaystyle f(n) = \Omega(n^{\log_b (a) + \epsilon})$$
同时存在常数$c < 1$以及充分大的$n$满足
$$
af(n/b)<cf(n)
$$
那么
$$\displaystyle T(n) = \Theta(f(n))$$
{% endnotel %}

> *课程之外，菜狗存而不论，数学定理，菜狗论而不证.*

我们先略过证明，简单解释一下上面的情况. 
事实上，我们讨论的就是$f(n)$的**阶**. 第一种情况，$f(n)$的上界是$O(n^{\log_b a - \epsilon})$，这就是说$f(n)$的阶数小于$\log_b a$，因此$T(n)$的时间复杂度就是$\displaystyle \Theta(n^{\log_b a})$. 而在第三种情况中，$f(n)$的下界是$O(n^{\log_b a + \epsilon})$，这就是说$f(n)$的阶数大于$\log_b a$，因此$T(n)$的时间复杂度取决于$f$，为$\Theta(f(n))$.

更加复杂的是：**如果$f$的阶数和等于$\log_b a$呢？** 事实上，如果$n$的阶数相同，我们还需要知道$\log n$的阶数. 关于更详细的内容，请参看详细证明.

{% notel green 证明 %}
未来再来探索吧
{% endnotel %}

## 例子

接下来我们回到一开始的那几道题，来体会一下主定理的强大：

![欢迎回来](/images/hw1-master-thm.png)

**Problem 4 (a)**

{% notel blue 解 %}
因为$\displaystyle \log_2 4 = 2 > 1$. 因此由主定理可知：
$$T(n) = \Theta(n^{\log_2 4}) = \Theta(n^2)$$ $\square$
{% endnotel %}

**Problem 4 (b)**

{% notel blue 解 %}
因为$log_4 2 = 1/2 = 1/2$. 因此存在$\epsilon \geq 0$，使得
$$\displaystyle \sqrt n = \Theta(n^{\log_2(4)} \log^{\epsilon}n)$$
所以
 $$\displaystyle T(n) = \Theta(\sqrt n \log^{\epsilon+1}n)$$
 而且在这里$\epsilon$可以任意小，所以事实上
 $$\displaystyle T(n) = \Theta(\sqrt n \log n)$$
{% endnotel %}

**Problem 4 \(c\)**

{% notel blue 解 %}
因为$\displaystyle \log_4 3 < 1$. 所以可以找到$\displaystyle \epsilon=\frac{1}{2}(1 - \log_4 3)$使得
 $$\displaystyle f(n) = \Omega(\displaystyle n^{\log_4 3 + \epsilon})$$
 因为$\Theta(n\lg n) = \Theta(n \log n)$，所以由主定理可知：
$$T(n) = \Theta(n \log n)$$$\square$
{% endnotel %}

**Problem 4 (d)**

{% notel blue 解 %}
因为$\log_2 9 \approx 3.17 > 3$. 所以由主定理可知
$$T(n)=\Theta(n^{log_2 9})$$$\square$
{% endnotel %}

## 总结

- 我们可将一个递归的程序形式化地表示为$T(n) = aT(n / b) + f(n)$，表示每进行一次递归就将规模为$n$的问题拆解为$a$个规模为$n / b$的小问题，每次拆分的代价为$f(n)$
- 主定理给出了有上面形式的递归程序的时间复杂度的计算方法
- 使用主定理进行计算需要分析$f(n)$的时间复杂度与$\Theta(n^{\log b a})$的大小关系


[^1]: 定理内容来自 [维基百科](https://zh.wikipedia.org/wiki/%E4%B8%BB%E5%AE%9A%E7%90%86)

[^2]: 题目来自清华大学自动化系数据结构课程作业