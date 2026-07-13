---
layout: single
title:  "Note: statistical inference (1)"
date:   2026-07-13 12:00:00 +0800
categories: probability-and-statistics
excerpt: "note: statistical inference (1)"
---

$$
\newcommand{\P}{\mathbb{P}}
\newcommand{\E}{\mathbb{E}}
\newcommand{\R}{\mathbb{R}}
\newcommand{\s}{\sigma}
\newcommand{\sA}{\mathscr{A}}
\newcommand{\sB}{\mathscr{B}}
\newcommand{\sF}{\mathscr{F}}
\newcommand{\sU}{\mathscr{U}}
$$



We define a **statistical model** to be a tuple $(X,\sF,P)$, where $X$ is the image space of some random variables, $\sF$ is a $\s$-algebra on $X$, and $P$ is a family of probability measures on $X$. Usually $X$ will be (a product of) Euclidean space. Often the probability measures will come from a parameter: $P = \{ P_\theta \}, \theta \in \Theta \subset \R^p$. In this case we call this a **parametric model**.

In practice of the statistical inference, often we are given the values of the random variables $(X_1, \dots, X_n)$ (a sample), theoretically $(X_1,\dots, X_n)$ satisfies one distribution $P_\theta$ on $X$, and we want to determine the parameter $\theta$, often by some functions of $X_1,\dots, X_n$. Such a (Borel-measurable) function $T(X_1,\dots,X_n)$ will be called a statistic.

The following type of parametric model will appear to have nice properties:

**Def. 1** A parametric model $(X,\sF,P)$ is called an **exponential family of distributions** if each $P_\theta$ admits a density or mass function $f(x;\theta)$ which is of the form

$$
f(x;\theta) = \exp(\eta(\theta)^T T(x) - \xi(\theta)) h(x)
$$

The **dimension** of this parametric model will be denoted as the dimension of the vector $T(x)$.

An exponential family of distribution is called **full-rank**, if the parametric space $\Theta$ contains an interior point in $\R^p$. $\square$

Examples: The binomial, Poisson, Gaussian distributions are all exponential families. (For example the mass function of Poisson distribution can be written as $\exp((\ln \theta) \cdot x - \theta) \cdot \frac{1}{k!}$)

Now we talk about the sufficient and complete statistics:

**Def.2 (sufficiency)** Given a parametric model $(X,\sF,P)$, a statistic $T$ (recall: this is a measurable function whose domain is $X$) is called **sufficient**, if for any nonnegative Borel function $f$, there exists a Borel function $h$, that the random variable $E(f(x) \vert T(x))$ equals to $h(T(x))$ a.e., for any parameter $\theta$. By informal language, this is to say that the conditional distribution of $X$ given $T(X)$ doesn't depend on $\theta$. $\square$

(Remark: the condition "nonnegative Borel" above can be replaced with "bounded Borel". Moreover, if $T$ is already known to be sufficient, then for any Borel function $h$, if $h$ is $L^1$ for one parameter $\theta$, then $h$ is $L^1$ for all parameters, and the statement above remains true for $h$.)

**Def.3** A sufficient statistic $T$ is called **minimal** if, for any sufficient statistic $S$, there exists a Borel function $f$ that $T = f(S) \text{ }P\text{-a.s.}$ Here $P\text{-a.s.}$ means that for any $\theta$, the statement is $P_\theta \text{-a.s.}$ true. $\square$

Examples: $T(x) = x$ is clearly a sufficient statistic. For a nontrivial example, consider $\Theta = {(a,b): a<b}, X = \R^n$, and let $P_\theta = P_(a,b)$ be the distribution of $(X_1,\dots,X_n)$, where $X_1,\dots, X_n$ are i.i.d. random variables of the distribution $\sU(a,b)$ (the uniform distribution). Suppose that we know one sample of $(X_1,\dots, X_n)$, and we arrange them as $X_{(1)}\leq X_{(2)} \leq \cdots \leq X_{(n)}$. If $X_{(1)}$ and $X_{(n)}$ are given, then the other variables satisfy a uniform distribution in $[X_{(1)},X_{(n)}]$, hence we can believe that the vector $(X_{(1)}, X_{(n)})$ is sufficient to determine $(a,b)$. In fact, it is a minimal sufficient statistic, which we'll see later.

Here are the theorems which determines sufficiency or the minimal condition:

**Thm.4 (Fisher–Neyman factorization theorem)** Suppose that all $P_\theta$ has density or mass functions $f_\theta$, then $T$ is sufficient if and only if, there exists measurable functions $g_\theta(x), h(x)$ that

$$
f_\theta(x) = g_\theta(T(x)) h(x).
$$

The proof of the general case of this theorem is notoriously long, which we will hence admit. $\square$

**Thm.5** Suppose that $X = \R^n$, $P_\theta$ has density function $f_\theta$, $T$ is sufficient and $h$ is a measurable function. Suppose that for any $x,y$ possible values of $X$, if "For any $\theta$, $f_\theta(x) = f_\theta(y) h(x,y)$" implies "$T(x)=T(y)$". Then $T$ is minimal.

**Cor.6** Suppose that $(X,\sF,P)$ is an exponential family of distributions, which has density function and has dimension $p$. We recall that

$$
f(x;\theta) = \exp(\eta(\theta)^T T(x) - \xi(\theta)) h(x)
$$

By the factorization theorem, $T$ is sufficient. Suppose that there exists $\theta_0,\dots, \theta_p \in \Theta$, that $\eta(\theta_i) - \eta(\theta_0)$ are linearly independent in $\R^p$, then $T$ is minimal. $\square$

**Proof of Thm.5** A theorem of Baradur guarantees that, in the case $X = \R^n$ and $P_\theta$ has density functions, a minimal sufficient statistic always exists, which we will denote by $S$. By the definition, there exists a measurable function $g$ that $S = g(T)$. By the factorization theorem, we write $f_\theta(x) = g_\theta(S(x)) l(x)$, then $l \neq 0 \text{ }P\text{-a.s.}$. We denote $h(x,y) = \frac{l(x)}{l(y)}$.

For any $x,y$ that $S(x) = S(y)$, we know that $f_\theta(x) = f_\theta(y) h(x,y)$ for any $\theta$. Hence $T(x) = T(y)$. Hence $l$ is a bijection in the range of $S$ and $T$, and hence $T$ is also minimal. $\square$

As a direct consequence of theorem 4 and 5, we see that in the previous example, $(X_{(1)}, X_{(n)})$ is indeed a minimal sufficient statistic.



**Def.7 (Completeness)** A statistic $T$ is called **complete**, if for any measurable function $h$, "For any $\theta$, $\E(h(T)) = 0$" implies "$h(T) = 0$ $P$-a.s.". $T$ is called **bounded complete**, if the measurable functions are replaced by the bounded measurable functions. $\square$

The following theorem builds one relation between completeness and sufficiency:

**Thm.8** Suppose that $T$ is finite-dimensional (the image of $T$ lies in Euclidean space), $T$ is bounded complete and sufficient, then $T$ is minimal.

Proof. Write $T = (T_1, \dots, T_k)$. For any sufficient statistic $S$, let $g_j(S) = \E(\arctan(T_j)\vert S), h_j(T) = \E(g_j(S)\vert T)$. Since $S, T$ are sufficient, $g_j, h_j$ don't depend on $\theta$. For any $\theta$, 

$$
\E(h_j(T)) = \E(g_j(S)) = \E(\arctan(T_j)).
$$

Hence by definition, $h_j(T) = \arctan(T_j)$ $P$-a.s. For any $\theta$,

$$
\begin{align}
Var(g_j(S)) = Var(\E(g_j(S) \vert T)) + \E(Var(g_j(S) \vert T)) \geq Var(h_j(T)) \\

Var(h_j(T)) = Var(\E(h_j(T) \vert S)) + \E(Var(h_j(T) \vert S)) \geq Var(g_j(S))
\end{align}
$$

Hence all the inequalities actually take equations, $Var(h_j(T) \vert S) = 0$. We deduce that

$$\E((h_j(T) - \E(h_j(T) \vert S))^2 \vert S) = 0, $$

hence $h_j(T) = \E(h_j(T) \vert S) = g_j(S)$. Hence $T_j = \tan(\arctan(T_j)) = \tan(g_j(S))$, $T$ is indeed minimal. $\square$

Here is one theorem for determining completeness, however in practice it's more often to just use the definition.

**Thm.9** Suppose that $(X,\sF,P)$ is an exponential family which is full-rank and $\eta(\theta) = \theta$, then $T$ is sufficient and complete.

The proof use some properties of the MGF (moment generating function), which we will admit. $\square$

The completeness help us determine some independence between random variables. To achieve this, we define first the ancillary statistics.

**Def.10** A statistic $T$ is called **ancillary** if for any nonnegative Borel function $h$, $\E(h(T))$ doesn't depend on the parameter $\theta$. It is called **first-order ancillary** if $\E(T)$ doesn't depend on the parameter. $\square$

Remark. The statement above remains true for bounded or $L^1$ Borel function $h$. See the remark of Def.2.

**Thm.11 (Basu)** Suppose that $V$ is **ancillary**, and $T$ is sufficient and complete. Then for any $\theta$, $V(x)$ and $T(x)$ are independent.

Proof. For any bounded Borel function $f$, $\E(f(V))$ doesn't depend on $\theta$, hence can be viewed as a constant. Since

$$
\E(\E(f(V)\vert T) - \E(f(V))) = 0,
$$

$\E(f(V)\vert T) = \E(f(V))$ for any $f$. By the properties of conditioning, $V$ is independent to $T$. $\square$

Example: As a direct consequence, suppose that $X_1,\dots, X_n$ are i.i.d. variables of distribution $\text{Exp}(a,\theta)$:

$$
f_{(a,\theta)}(x) = \frac{1}{\theta} \exp(-\frac{x - a}{\theta}) 1_{x\geq a}
$$

Then for any $1\leq k \leq n$, the three variables

$$
\frac{X_{(n)} - X_{(k)}}{X_{(n)} - X_{(n-1)}}, X_{(1)}, \sum_{i=1}^{n} {(X_i - X_{(1)})}
$$

are independent.

