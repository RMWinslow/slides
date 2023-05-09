---
layout: presentation
title: Branching Problems and PGFs
---

name: inverse
class: center, middle, inverse


# Branching Problems and PGFs

---

## The Probability Generating Function

$X$ is a discrete random variable with support $\mathbb{Z}_{\geq 0}$ 
and probability mass function $p_X$. 
Then we define the probability generating function $G_X(🙂)$ as

$$G_X(🙂)\equiv E[🙂^X] = \sum\_{x=0}^\infty \left[ p\_X (x) \cdot 🙂^x \right]$$

---

## Useful Properties of the PGF

### We can easily sum variables: 

If $Y$ and $W$ are independent (discrete random variables with support $\mathbb{Z}_{\geq 0}$), and $X\sim aY + bW$, then 

$$G_X(😬)=G\_Y(😬^a)\cdot G\_W(😬^b)$$

---

## Useful Properties of the PGF


### We can easily sum variables.

- In particular, if $x\_1,X\_2,...,X\_N$ are iid, and $Y\sim \sum\_i X\_i$, then

$$G\_Y(🙂) = [G\_X(🙂)]^N$$

---

## Useful Properties of the PGF

### Compound Distributions

If $N$ itself is a discrete random variables with support $\mathbb{Z}_{\geq 0}$, 
which is independent of $X\_i$, 
and if $Y\sim \sum^N\_{i=1} X_i$ is the sum of $N$ iid draws of $X$, then 

$$G\_Y(🙂) = G\_N(G\_X(🙂))$$

---

## Useful Properties of the PGF

### Compound Distributions

If $N$ itself is a discrete random variables with support $\mathbb{Z}_{\geq 0}$, 
which is independent of $X_i$, 
and if $Y\sim \sum^N\_{i=1} X_i$ is the sum of $N$ iid draws of $X$, then 

$G_Y(🙂) = G\_N(G\_X(🙂))$

In particular, if $N$ is iid to $X$, then 

$$G_Y(🙂) = G\_X(G\_X(🙂))$$

---

## Useful Properties of the PGF

### Moments

Derivative wrt 🙂 is $\sum_{x=0}^\infty \left[x \cdot p\_X (x) \cdot 🙂^{x-1} \right]$  and therefore 

$$G^\prime(1)=E[X]$$


---

## Useful Properties of the PGF

### Moments

Derivative wrt 🙂 is $\sum_{x=0}^\infty \left[x \cdot p\_X (x) \cdot 🙂^{x-1} \right]$  and therefore 

$$G^\prime(1)=E[X]$$

And in general, the $n$th derivative gives the $n$th factorial moment. 

$$G^{\prime n} (1) = E\left[\frac{x^!}{(x-r)!}\right]$$

---

## Useful Properties of the PGF

### Zeros:

$$G_X(0) = \sum\_{x=0}^\infty \left[ p\_X (x) \cdot 0^x \right] = p\_0$$

---

## Useful Properties of the PGF

Note that if $X$ is a constant random variable equal to 1, then 

$$G_x(🙂) = \sum\_{x=0}^\infty \left[ p\_X (x) \cdot 🙂^x \right]$$

$$G_x(🙂) =  🙂$$

This also means that the pgf for $1+Y$ is $🙂\cdot G_Y(🙂)$



---

## Useful Properties of the PGF

Also we can get the pmf back out

$$p_X(x) = \frac{1}{k!}\frac{\partial^k}{\partial x^k} G\_0 |\_{x=0}$$





---

## Applications to Branching Problems

- Start with a single individual.
- This individual has offspring distribution $Z$
- All of their descendents also have iid offspring distributions $Z$


---

## Applications to Branching Problems


If $G=G_Z$, and the 0th generation has 1 individual, then
- The number of descendents in the first generation has generating function $G(🙂)$
- '' in the second generation '' $G(G(🙂)) = G^2(🙂)$
- '' in the third generation '' $G(G((🙂))) = G^3(🙂)$
- '' in the $g$th generation is $G^g(🙂)$

---

## Applications to Branching Problems

### Extinction

- $G(0)$ gives the chance that the initial individual will have no children
- $G(G(0))$ gives the chance they will have no grandchildren
- $G^g(0)$ gives the chance that the lineage will have died out by generation $g$.


---

## Applications to Branching Problems

### Extinction

The chance that the lineage will ultimately go extinct is 

$$\lim_{g\to\infty} G^g(0) = G^\infty(0)$$

---

## Applications to Branching Problems

### Extinction

The chance that the lineage will ultimately go extinct is 

$$\lim_{g\to\infty} G^g(0) = G^\infty(0)$$

- Note that $G^\infty$ has the property that $G^\infty(0)=G(G^\infty(0))$, 
- and that there is at most one $💀\in (0,1)$ such that $G(💀)=💀$
- Iff $\mu_Z = G^\prime(1)\geq 1$, then there is a unique positive solution for $G^\infty(0)$ $\in(0,1)$
- If $\mu_X < 1$, then $G^\infty(0)=1$ 



















---

## Example Paper 1: 

### Superspreading and the effect of individual variation on disease emergence

2005 Nov - J. O. Lloyd-Smith, S. J. Schreiber, P. E. Kopp & W. M. Getz  

---

### Superspreading and the effect of individual variation on disease emergence

- Each individual $x$ is assumed to spread disease according to a Poisson process with individual specific mean $v_x$. 
- These individual attack rates are Gamma-distributed 
- The Gamma-Poisson mixture distribution has pgf

$G_Z(🙂) = \left(\left(1-🙂\right)\frac{R_{0}}{k}+1\right)^{-k}$

- High dispersion parameter $k$ makes outbreaks more volatile. Has implications for the targetting of government intervention





---

## Example Paper 2: 

### Spread of epidemic disease on networks

M. E. J. Newman



---

### Spread of epidemic disease on networks

- The degree distribution of nodes has mean $z$ and  pgf labelled $G_0$
- Choose a random edge, and travel to one of it's endpoints. The degree distribution of such nodes is labelled $G_1$ and $G_1(x)=\frac{G^\prime(0)}{z}$.
- Edge percolation: edges are removed iid with probability $1-T$
  - Degree distribution of non-removed edges is labelled $G_0(x;T)$
  - Degree distribution of non-removed edges of nodes reachable by travelling along a random non-remove edge is labelled $G_1(x;T)$

- Relationships are establish between these distributions.




---
