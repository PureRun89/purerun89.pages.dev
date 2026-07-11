---
layout: single
title:  "Note: conditional expectation"
date:   2026-07-11 23:00:00 +0800
categories: probability-and-statistics
---


The conditioning seems to be widely used in the theory of statistics, hence it might be useful to learn its basics before straightly diving into statistics.

$$
\newcommand{\P}{\mathbb{P}}
\newcommand{\E}{\mathbb{E}}
\newcommand{\s}{\sigma}
\newcommand{\A}{\mathscr{A}}
\newcommand{\B}{\mathscr{B}}
$$

We firstly give several definitions of conditioning:

**Def.1 (Conditioning of $L^1$ variable)** Suppose the space of probability $(\Omega, \mathscr{A}, \P)$. Given a random variable $X \in L^1(\Omega)$ and $\s$-algebra $\B \subset \A$, the conditional expectation of $X$ given $\B$ is uniquely (in a.e. sense) defined by a $\B$-measurable random variable $\E(X\vert \B) \in L^1$, such that for any $\B$-measurable bounded random variable $Z$,

$$
\E(XZ) = \E(\E(X\vert \B) Z).
$$

To demonstrate this, we consider the measure on $(\Omega, \B)$ defined by $B \mapsto \int_B X \P(d\omega)$, which is a signed measure controlled by $\P$. By the Radon-Nikodym theorem, there exists a $\B$-measurable function $f$ that the measure defined above is $f \cdot \P$. We denote $\E(X \vert \B) = f$, and the statement above can be proved by approximating $Z$ with sums of characteristic functions $1_B$.

For arbitrary $X \in L^1$, it suffices to decompose $X$ into its positive and negative parts, and go through the same proof. The uniqueness of $\E(X \vert B)$ easily follows. $\square$

**Def.2 (Conditioning of nonnegative variable)** Given a random variable $X \geq 0$ and $\s$-algebra $\B$, we can define the nonnegative $\B$-measurable variable $\E(X\vert \B)$ such that for any nonnegative $\B$-measurable random variable $Z$,

$$
\E(XZ) = \E(\E(X\vert \B) Z). \square
$$

The concrete construction is to consider $0\leq X_1\leq X_2 \leq \cdots \rightarrow X$, such that each $X_i$ is bounded. Then $\E(X_i\vert B)$ converge to the demanded $\E(X\vert \B)$.

Note that even if $X$ is finite a.s., its condition expectation can equal to $+\infty$ a.s..

Generally, the conditioning on a variable $X$ is somewhat taking its average value on every set of points which can't be distinguished by $\B$. When $\B$ is induced by another random variable $Y$, we denote the conditioning by $\E(X\vert Y)$. In fact, there is a unique (in a.e. sense) Borel function $f$ that $\E(X\vert Y) = f(Y)$, according to the following lemma, whose proof is fully measure-theoretic and technique:

**Lem.3 (Doob-Dynkin)** Suppose that $T: \Omega \rightarrow (\Omega', \mathscr{M})$, where $(\Omega', \mathscr{M})$ is a space with its $\s$-algebra. We define the $\s$-algebra on $\Omega$ by $\sigma(T) := T^{-1}(\mathscr{M})$. Suppose $f: \Omega \rightarrow \mathbb{R}$. (We consider the Borel algebra instead of the Lebesgue one). Then,

$f$ is measurable if and only if there exists $g$ measurable, $f = g\circ T$. $\square$

Hence the conditioning of $X$ given another variable $Y$ is a variable $f(Y)$ which best approximates $X$.

**Prop.4** When $X$ is in $L^2$, the conditioning of $X$ can also be realized by orthogonal projection: $L^2(\A)$ is a Hilbert space, and $L^2(\B)$ is its closed subspace. By definition, for any $Z \in L^2(\B)$, $\E(Z (X - \E(X\vert \B))) = 0$, hence $\E(X\vert \B))$ is the orthogonal projection of $X$. $\square$

The conditional variance is defined in a similar way of defining variance:

**Def.5 (Conditional variance)** $X \in L^2$.

$$
Var(X\vert \B) := \E(X^2 \vert \B) - \E(X \vert B)^2. \square
$$

Now there are some general properties of conditioning:

**Prop.6**

- $\E(\E(X\vert \B)) = \E(X)$. (Total expectation)
- If $X$ is $\B$-measurable, $\E(X\vert \B) = X$.
- $\lvert \E(X\vert \B) \rvert \leq \E(\lvert X \rvert \vert \B)$.
- $\B_1 \subset \B_2$, then $\E(\E(X \vert \B_2) \vert \B_1) = \E(X \vert \B_1)$.

(Conditional expectation looks like expectation:)
- $X_n \geq 0$, then $\E(\text{lim inf } X_n \vert \B) \leq \text{lim inf } \E(X_n \vert \B)$.
- $f\geq 0$ convex, and $X \in L^1$, then $\E(f(X) \vert \B) \leq f(\E(X \vert \B))$. $\square$


**Prop.7 (Independence)** $\B_1$ and $\B_2$ are independent if and only if, for any $\B_2$-measurable positive variable $X$,

$$
\E(X\vert \B_1) = \E(X) \square
$$

The conditioning $\E(X\vert Y)$ is easy to compute, when the total space is discrete, or $X$ is already a function of $Y$, or when $(X,Y)$ has a density:

**Prop.8 (Computation in the density case)** Suppose the density of $(X,Y)$ is $p(x,y), x \in \mathbb{R}^m ,y \in \mathbb{R}^n$. Let the density of $Y$ be $q(y) = \int p(x,y) dx$. For nonnegative Borel function $h$, Let

$$
\phi(y) = \frac{1}{q(y)} \int {h(x) p(x,y) dx} \text{ if } q(y)\neq 0
$$

(If $q(y)= 0$, $\phi(y)$ can be arbitrary) Then $\E(h(X)\vert Y) = \phi(Y)$. $\square$

**Prop. 9** Under the same hypothesis of the preceding proposition, for $y \in \mathbb{R}^n$, define the measure of probability:

$$
\nu(y,dx) =
\begin{cases}
\frac{1}{q(y)} p(x,y)dx, \text{ if } q(y)>0, \\
\delta_0(dx), \text{ if } q(y) = 0
\end{cases}
$$

Then for any nonnegative Borel function $h$,

$$
\E(h(X,Y)\vert Y) = \int_{\mathbb{R}^m} h(x,Y) \nu(Y,dx).
$$

Proof. By Doob-Dynkin lemma, it suffices to verify that for any nonnegative Boren function $f$, 

$$
\begin{align}
\E(h(X,Y)f(Y)) = \int h(x,y) f(y) p(x,y) dx dy \\
= \int_{\mathbb{R}^n} f(y) q(y) (\int h(x,y) \nu(y,dx)) dy \\
= \E(((x,y) \mapsto \int_{\mathbb{R}^m} h(x,y) \nu(y,dx)) \cdot f(Y)) \square
\end{align}
$$

Remark. The two propositions above can be extended to any Borel $h$ with good integrability conditions. Just write $h = h_+ - h_-$ and finish the proof.

