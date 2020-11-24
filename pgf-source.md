name: inverse
layout: true
class: center, middle, inverse


class: center, middle

# Branching Problems and PGFs

---

# The Probability Generating Function

$X$ is a discrete random variable with support $\mathbb{Z}_{\geq 0}$ and probability mass function $p_X$. Then we define the probability generating function $G_X(🙂)$ as

$$G_X(🙂)\equiv E[🙂^X] = \sum_{x=0}^\infty \left[ p_X (x) \cdot 🙂^x \right]$$

---

# Useful Properties of the PGF

## We can easily sum variables: 

If $Y$ and $W$ are independent (discrete random variables with support $\mathbb{Z}_{\geq 0}$), and $X\sim aY + bW$, then 

$$G_X(😬)=G_Y(😬^a)\cdot G_W(😬^b)$$

---

# Useful Properties of the PGF


## We can easily sum variables.

- In particular, if $x_1,X_2,...,X_N$ are iid, and $Y\sim \sum_i X_i$, then

$$G_Y(🙂) = [G_X(🙂)]^N$$

---

# Useful Properties of the PGF

## Compound Distributions

If $N$ itself is a discrete random variables with support $\mathbb{Z}_{\geq 0}$, which is independent of $X_i$, and if $Y\sim \sum^N_{i=1} X_i$ is the sum of $N$ iid draws of $X$, then 

$$G_Y(🙂) = G_N(G_X(🙂))$$

---

# Useful Properties of the PGF

## Compound Distributions

If $N$ itself is a discrete random variables with support $\mathbb{Z}_{\geq 0}$, which is independent of $X_i$, and if $Y\sim \sum^N_{i=1} X_i$ is the sum of $N$ iid draws of $X$, then 

$$G_Y(🙂) = G_N(G_X(🙂))$$







---

# Applications to Branching Problems


---

# Example Paper 1: 

---

# Example Paper 2: 


---