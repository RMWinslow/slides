---
title: "Office Hours: 2023 Sept 07 (kjetil presentation)"
layout: presentation_solar
parent: PUI
---

class:middle

# PUI Presentation, Sept 07, 2023

Robert Winslow

What is the effect of partial unemployment insurance on labor decisions?












---

layout: true
class: header

<h2 style="background-color: #dfd;">Partial Unemployment Insurance in the US</h2>

---


### State UI Recipients Over Time, All US

<img src="img/20230505/saUSAwide.png" style="max-width:100%;">

---

### Partial Unemployment Insurance

- If a person is eligible for UI, a weekly benefit amount (WBA) is determined based on employment history.
  - Except for high earners, it's about half of their typical income.
  - Constant throughout entire UI spell.
- Benefits depend both on the current week's gross earnings, and on the individual's WBA.
  - Your WBA is the amount you collect when totally unemployed.
  - As earnings increase, benefits decrease
  - Details vary by state.
- During the pandemic, the Federal Pandemic Unemployment Compensation supplement (600 then later 300 USD) was paid out in full to anyone collecting even a single dollar of state UI.


---

### Example: State UI Benefits in Minnesota

<img src="img/20230505/uiMN.png" style="max-width:40%;float:right;">

In Minnesota, the rule is that the benefits for a given week are determined by:

$$
benefits = \begin{cases}
WBA - \frac{earnings}{2} &\text{ if } earnings < WBA \\
0 &\text{ if } earnings \geq WBA \\
\end{cases}
$$

where WBA is weekly benefit amount (person-specific, fixed for entire duration of benefits spell)
and the earnings refers to the current week's labor income before taxes and transfers.

*Figure on right: earnings and benefits for a hypothetical Minnesota worker with a WBA of 400 USD*


<!--TODO: What was YIRU's WBA? I should plug that in here instead of a generic 400.-->

---



### State UI Recipients Over Time, MN

<img src="img/20230505/saMNwide.png" style="max-width:100%;">

---





























---

layout: true
class: header

<h2 style="background-color: #eef;">Model</h2>

---

- Simple model of job search and unemployment insurance.
- Based on:
    - *The role of unemployment insurance in an economy with liquidity constraints and moral hazard* (Hansen, Imrohoroğlu, 1992)
    - *Unemployment insurance and the role of self-insurance.* (Abdulkadiroğlu, Kuruşçu, Şahin, 2002).
- My contribution is the addition of *partial* unemployment insurance.


<!--The following are some global definitions for more concise notation.-->

$$
\gdef\etaE{\text{E}}
\gdef\etaP{\text{P}}
\gdef\etaU{\text{U}}
\gdef\sE{e}
\gdef\sP{p}
\gdef\sU{u}
\gdef\hP{\hat{h}_p}
\gdef\hE{\hat{h}_e}
$$


---


### Consumer's choices

The consumer's optimand is straightforward:

$$\mathbb{E} \sum_j \beta^t U(c_t,l_t) = 
\mathbb{E} \sum_t \beta^t \Big(\frac{c_t^{1-\gamma_c}}{1-\gamma_c} + \psi \cdot \frac{l_t^{1-\gamma_l}}{1-\gamma_l}\Big)$$

Two decisions the consumer faces:

1. How to split income between consumption and (non-interest-bearing) savings
    - budget is $m'+c = m+y_d$, where $m$ is assets, and $y_d$ is disposable income.
    - assets are subject to the constraint $m'\geq 0$

2. Whether and how much to work when give a job opportunity. (See next slide.)

<!--These basics are very similar to (Abdulkadiroğlu, Kuruşçu, Şahin, (2002)).-->

---


### Job Search



- Employment opportunity $s\in\set{e,p,u}$ represents whether the person has a job opportunity ($s=e$), a partial job opportunity ($s=p$) or no job opportunity ($s=u$). (Employment, Partial employment, full Unemployment)
    - $s$ evolves according to a 3x3 transition matrix $\chi$, <!--TODO: Calibrate-->

$$\chi = 
\begin{bmatrix}
   \chi(e,e) & \chi(e,p) & \chi(e,u) \\
   \chi(p,e) & \chi(p,p) & \chi(p,u) \\
   \chi(u,e) & \chi(u,p) & \chi(u,u) 
\end{bmatrix}
$$

- employment status $\eta\in\Set{\etaE,\etaP,\etaU}$ represents the level of work the consumer actually chooses to engage in. 
    - If $s=\sE$, consumer can choose from $\eta\in\Set{\etaE,\etaP,\etaU}$
    - If $s=\sP$, consumer can choose from $\eta\in\Set{\etaP,\etaU}$
    - If $s=\sU$, consumer must choose $\eta = \etaU$


<!--
- Note that $s=u \implies \eta=0$. But if the person chooses not to accept an employment opportunity, $(s,\eta)=(e,0)$.
-->


---

### Unemployment Benefits

$\mu\in\set{0,1}$ is a binary variable indicating whether the person collects unemployment benefits.

- If $s=\sE$, then $\mu=0$
- If $(s,\eta)=(\sP,\etaP)$ or $(\sU,\etaU)$, then $\mu=1$
- If $\eta=\etaU$, but $s\neq\sU$, then $\mu=1$ with probability $\pi_u$, 0 otherwise
- If $\eta=\etaP$, but $s\neq\sP$, then $\mu=1$ with probability $\pi_p$, 0 otherwise

If Consumer collects benefits, the benefits adjust their disposable income to some fraction of employed disposable income, called the "replacement rate".

-  $\theta_p$ is replacement rate for partially employed (when $(\eta,\mu)=(\etaP,1)$)
-  $\theta_u$ is replacement rate for unemployed (when $(\eta,\mu)=(\etaU,1)$)


<!--TODO?: Make pi dependent on s, eta, and previous s or eta?-->

---

### Utility Flows, Income, and Leisure

Given $(m,m',\eta,\mu)$, utility flow is:

$$U\Big(m-m'+y_d(\eta,\mu),\;l(\eta)\Big)$$

where

$$
y_d(\eta,\mu) =
\begin{cases}
   (1-\tau)y                &\text{if } (\eta,\mu)=(\etaE,0) \\
   (1-\tau)yθ_p             &\text{if } (\eta,\mu)=(\etaP,1) \\
   (1-\tau)yθ_u             &\text{if } (\eta,\mu)=(\etaU,1) \\
   (1-\tau)y\frac{\hP}{\hE} &\text{if } (\eta,\mu)=(\etaP,0) \\
   0                        &\text{if } (\eta,\mu)=(\etaU,0) \\
\end{cases}
$$

and

$$
l(\eta) =
\begin{cases}
   1-\hE &\text{if } \eta=\etaE \\
   1-\hP &\text{if } \eta=\etaP \\
   1 &\text{if } \eta=\etaU \\
\end{cases}
$$

---

### Timeline Within Each Period



1. Consumer recieves potential job offer $s\in\set{e,p,u}$
2. Consumer chooses employment status $\eta\in\Set{\etaE,\etaP,\etaU}$
3. Draw $\mu\in\set{0,1}$: does Consumer get unemployment benefits?   
4. Consumer chooses $m'$ after seeing $\mu$




---

### Value Functions

$$
V(e,m) = \max_{\eta\in\set{\etaE,\etaP,\etaU}}\Big\lbrace
\mathbb{E} \left[\max_{m'}\Set{U(m-m'+y_d(\eta,\mu),l(\eta))+cont(e,m')}\right]
\Big\rbrace
$$

$$
V(p,m) = \max_{\eta\in\set{\etaP,\etaU}}\Big\lbrace
\mathbb{E} \left[\max_{m'}\Set{U(m-m'+y_d(\eta,\mu),l(\eta))+cont(p,m')}\right]
\Big\rbrace
$$

$$
V(u,m) = \max_{m'}\Set{U(m-m'+y_d(\eta,\mu),l(\eta))+cont(u,m')}
$$

where

$$cont(s,m') \equiv \beta \sum_{s'}\chi(s,s')V(m',s')$$


---


### Market Clearing and Equilibrium

State of a person is $x=(m,s,\eta,\mu)$

Stationary equilibrium consists of 
- decision rules $\eta(m,s)$, $c(x)$, $m'(x)$
- time-invariant measure $\lambda(x)$ of people in state $x$
- tax rate $\tau$

Such that

- Given $\tau$, the decision rules are optimal for the consumers.
- Goods market clears: 

$$\sum_x \lambda(x) c(x) = \sum_x \lambda(x) \cdot 
\begin{cases}
y                &\text{if }\eta=\etaE\\
\frac{\hP}{\hE}y &\text{if }\eta=\etaP\\
0                &\text{if }\eta=\etaU\\
\end{cases}
$$

- $\lambda(x')=\lambda(x)$
- Government budget  balanced (?):





































---

layout: true
class: header

<h2 style="background-color: #fee;">Calibration</h2>


---

### ψ=0.5, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 2.7731 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 62.02 | 2.8546 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.7%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **5.0%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 3.5399 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 3.6444 | 70% | 21% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **84.4%** | **88.8%** | **88.8%** | **88.8%** | **70.1%** |
| **Partly employed**  | **83.1%** | **9.3%** | **4.9%** | **4.9%** | **4.9%** | **21.4%** |
| Offered e, chose P  | 78.2% | 4.4% | 0.0% | 0.0% | 0.0% | 16.5% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **16.9%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **8.4%** |
| Offered e, chose U  | 10.6% | 0.0% | 0.0% | 0.0% | 0.0% | 2.1% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 4.01% | -0.0 | 4.3104 | 78% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **44.4%** | **79.4%** | **88.8%** | **88.8%** | **88.8%** | **78.0%** |
| **Partly employed**  | **2.2%** | **3.0%** | **4.9%** | **4.9%** | **4.9%** | **4.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 2.2% | 3.0% | 4.9% | 4.9% | 4.9% | 4.0% |
| **Unemployed**  | **53.4%** | **17.6%** | **6.3%** | **6.3%** | **6.3%** | **18.0%** |
| Offered e, chose U  | 44.4% | 9.4% | 0.0% | 0.0% | 0.0% | 10.7% |
| Offered p, chose U  | 2.7% | 1.9% | 0.0% | 0.0% | 0.0% | 0.9% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 4.01% | 115.18 | 4.4686 | 51% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **3.5%** | **75.0%** | **88.8%** | **88.8%** | **51.2%** |
| **Partly employed**  | **17.1%** | **71.0%** | **18.5%** | **4.9%** | **4.9%** | **23.3%** |
| Offered e, chose P  | 12.2% | 66.1% | 13.6% | 0.0% | 0.0% | 18.4% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **82.9%** | **25.5%** | **6.5%** | **6.3%** | **6.3%** | **25.5%** |
| Offered e, chose U  | 76.6% | 19.1% | 0.2% | 0.0% | 0.0% | 19.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 5.81% | 0.0 | 5.1116 | 60% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **20.3%** | **40.3%** | **62.9%** | **88.8%** | **88.8%** | **60.2%** |
| **Partly employed**  | **1.1%** | **3.0%** | **2.9%** | **3.6%** | **4.9%** | **3.1%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.1% | 3.0% | 2.9% | 3.6% | 4.9% | 3.1% |
| **Unemployed**  | **78.7%** | **56.7%** | **34.2%** | **7.7%** | **6.3%** | **36.7%** |
| Offered e, chose U  | 68.5% | 48.5% | 25.9% | 0.0% | 0.0% | 28.6% |
| Offered p, chose U  | 3.9% | 1.9% | 2.0% | 1.3% | 0.0% | 1.8% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 5.81% | 141.76 | 5.3276 | 34% | 20% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **10.0%** | **69.7%** | **88.8%** | **33.7%** |
| **Partly employed**  | **9.2%** | **23.8%** | **58.4%** | **4.9%** | **4.9%** | **20.3%** |
| Offered e, chose P  | 4.3% | 18.9% | 53.5% | 0.0% | 0.0% | 15.3% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **90.8%** | **76.2%** | **31.5%** | **25.4%** | **6.3%** | **46.0%** |
| Offered e, chose U  | 84.5% | 69.9% | 25.2% | 19.1% | 0.0% | 39.7% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 2.7731 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 97.46 | 2.865 | 72% | 22% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **4.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.8%** |
| **Partly employed**  | **89.6%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **21.9%** |
| Offered e, chose P  | 84.7% | 0.0% | 0.0% | 0.0% | 0.0% | 16.9% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.4% | -0.0 | 3.5398 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **2.1%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.4%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 2.1% | 4.9% | 4.9% | 4.9% | 4.9% | 4.4% |
| **Unemployed**  | **9.1%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.9%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 2.8% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.4% | 132.9 | 3.6762 | 56% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **12.0%** | **88.8%** | **88.8%** | **88.8%** | **55.7%** |
| **Partly employed**  | **20.0%** | **79.9%** | **4.9%** | **4.9%** | **4.9%** | **22.9%** |
| Offered e, chose P  | 15.1% | 75.0% | 0.0% | 0.0% | 0.0% | 18.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **80.0%** | **8.1%** | **6.3%** | **6.3%** | **6.3%** | **21.4%** |
| Offered e, chose U  | 73.7% | 1.8% | 0.0% | 0.0% | 0.0% | 15.1% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 4.81% | -0.0 | 4.309 | 73% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **34.7%** | **66.2%** | **88.8%** | **88.8%** | **88.8%** | **73.4%** |
| **Partly employed**  | **1.2%** | **1.5%** | **2.2%** | **4.9%** | **4.9%** | **2.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.2% | 1.5% | 2.2% | 4.9% | 4.9% | 2.9% |
| **Unemployed**  | **64.1%** | **32.3%** | **9.1%** | **6.3%** | **6.3%** | **23.6%** |
| Offered e, chose U  | 54.1% | 22.6% | 0.0% | 0.0% | 0.0% | 15.3% |
| Offered p, chose U  | 3.7% | 3.4% | 2.7% | 0.0% | 0.0% | 2.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 4.81% | 177.20000000000002 | 4.5226 | 43% | 8% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **38.4%** | **88.8%** | **88.8%** | **43.2%** |
| **Partly employed**  | **8.3%** | **17.2%** | **4.9%** | **4.9%** | **4.9%** | **8.1%** |
| Offered e, chose P  | 3.4% | 12.3% | 0.0% | 0.0% | 0.0% | 3.2% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **91.7%** | **82.8%** | **56.7%** | **6.3%** | **6.3%** | **48.7%** |
| Offered e, chose U  | 85.3% | 76.4% | 50.4% | 0.0% | 0.0% | 42.4% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 8.4% | -0.0 | 5.1093 | 52% | 2% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **11.9%** | **27.9%** | **50.7%** | **81.6%** | **88.8%** | **52.2%** |
| **Partly employed**  | **0.3%** | **1.0%** | **1.7%** | **1.5%** | **4.9%** | **1.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.3% | 1.0% | 1.7% | 1.5% | 4.9% | 1.9% |
| **Unemployed**  | **87.8%** | **71.1%** | **47.5%** | **16.9%** | **6.3%** | **45.9%** |
| Offered e, chose U  | 76.9% | 60.9% | 38.0% | 7.2% | 0.0% | 36.6% |
| Offered p, chose U  | 4.6% | 3.9% | 3.2% | 3.4% | 0.0% | 3.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 8.4% | 212.64 | 5.3963 | 27% | 6% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **5.1%** | **39.5%** | **88.8%** | **26.7%** |
| **Partly employed**  | **5.8%** | **9.0%** | **4.9%** | **4.9%** | **4.9%** | **5.9%** |
| Offered e, chose P  | 0.9% | 4.1% | 0.0% | 0.0% | 0.0% | 1.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.2%** | **91.0%** | **90.0%** | **55.6%** | **6.3%** | **67.4%** |
| Offered e, chose U  | 87.9% | 84.7% | 83.7% | 49.3% | 0.0% | 61.1% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.46% | -0.0 | 2.7724 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **2.0%** | **3.7%** | **4.9%** | **4.9%** | **4.9%** | **4.1%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 2.0% | 3.7% | 4.9% | 4.9% | 4.9% | 4.1% |
| **Unemployed**  | **9.2%** | **7.5%** | **6.3%** | **6.3%** | **6.3%** | **7.1%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 2.9% | 1.2% | 0.0% | 0.0% | 0.0% | 0.8% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.46% | 194.92 | 2.9124 | 54% | 14% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **4.8%** | **88.8%** | **88.8%** | **88.8%** | **54.2%** |
| **Partly employed**  | **11.4%** | **43.3%** | **4.9%** | **4.9%** | **4.9%** | **13.9%** |
| Offered e, chose P  | 6.4% | 38.4% | 0.0% | 0.0% | 0.0% | 9.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **88.6%** | **51.9%** | **6.3%** | **6.3%** | **6.3%** | **31.9%** |
| Offered e, chose U  | 82.3% | 45.6% | 0.0% | 0.0% | 0.0% | 25.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 4.35% | -0.0 | 3.5329 | 86% | 2% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **76.2%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **86.3%** |
| **Partly employed**  | **0.5%** | **0.7%** | **1.1%** | **1.6%** | **3.8%** | **1.5%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.5% | 0.7% | 1.1% | 1.6% | 3.8% | 1.5% |
| **Unemployed**  | **23.3%** | **10.5%** | **10.2%** | **9.7%** | **7.4%** | **12.2%** |
| Offered e, chose U  | 12.5% | 0.0% | 0.0% | 0.0% | 0.0% | 2.5% |
| Offered p, chose U  | 4.4% | 4.2% | 3.8% | 3.3% | 1.1% | 3.4% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 4.35% | 283.52 | 3.7722 | 39% | 6% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **16.5%** | **88.8%** | **88.8%** | **38.8%** |
| **Partly employed**  | **6.2%** | **7.6%** | **4.9%** | **4.9%** | **4.9%** | **5.7%** |
| Offered e, chose P  | 1.2% | 2.7% | 0.0% | 0.0% | 0.0% | 0.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **93.8%** | **92.4%** | **78.6%** | **6.3%** | **6.3%** | **55.5%** |
| Offered e, chose U  | 87.5% | 86.1% | 72.3% | 0.0% | 0.0% | 49.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 8.84% | -0.0 | 4.294 | 61% | 1% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **12.1%** | **39.6%** | **75.0%** | **88.8%** | **88.8%** | **60.9%** |
| **Partly employed**  | **0.2%** | **0.3%** | **0.5%** | **0.7%** | **1.2%** | **0.6%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.2% | 0.3% | 0.5% | 0.7% | 1.2% | 0.6% |
| **Unemployed**  | **87.7%** | **60.1%** | **24.5%** | **10.6%** | **10.1%** | **38.6%** |
| Offered e, chose U  | 76.7% | 49.2% | 13.8% | 0.0% | 0.0% | 27.9% |
| Offered p, chose U  | 4.7% | 4.6% | 4.4% | 4.3% | 3.8% | 4.3% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 8.84% | 345.54 | 4.6437 | 22% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **0.0%** | **19.3%** | **88.8%** | **21.6%** |
| **Partly employed**  | **5.2%** | **5.6%** | **6.7%** | **4.9%** | **4.9%** | **5.5%** |
| Offered e, chose P  | 0.3% | 0.7% | 1.8% | 0.0% | 0.0% | 0.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.8%** | **94.4%** | **93.3%** | **75.8%** | **6.3%** | **72.9%** |
| Offered e, chose U  | 88.5% | 88.1% | 87.0% | 69.5% | 0.0% | 66.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 20.48% | -0.0 | 5.0686 | 32% | 0% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.7%** | **5.5%** | **20.8%** | **43.8%** | **88.8%** | **31.9%** |
| **Partly employed**  | **0.0%** | **0.1%** | **0.2%** | **0.4%** | **0.6%** | **0.2%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.0% | 0.1% | 0.2% | 0.4% | 0.6% | 0.2% |
| **Unemployed**  | **99.3%** | **94.4%** | **79.0%** | **55.8%** | **10.6%** | **67.8%** |
| Offered e, chose U  | 88.1% | 83.3% | 68.0% | 44.9% | 0.0% | 56.9% |
| Offered p, chose U  | 4.9% | 4.8% | 4.7% | 4.6% | 4.3% | 4.7% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 20.48% | 354.40000000000003 | 5.4781 | 11% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **0.0%** | **1.3%** | **54.4%** | **11.2%** |
| **Partly employed**  | **5.1%** | **5.1%** | **5.4%** | **4.9%** | **4.9%** | **5.1%** |
| Offered e, chose P  | 0.1% | 0.2% | 0.5% | 0.0% | 0.0% | 0.2% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.9%** | **94.9%** | **94.6%** | **93.7%** | **40.7%** | **83.8%** |
| Offered e, chose U  | 88.6% | 88.5% | 88.2% | 87.4% | 34.4% | 77.4% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 2.5 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 62.02 | 2.5815 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 2.9937 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 3.0934 | 71% | 21% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **2.1%** | **88.7%** | **88.8%** | **88.8%** | **88.8%** | **71.4%** |
| **Partly employed**  | **83.3%** | **5.0%** | **4.9%** | **4.9%** | **4.9%** | **20.6%** |
| Offered e, chose P  | 78.4% | 0.0% | 0.0% | 0.0% | 0.0% | 15.7% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **14.6%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **8.0%** |
| Offered e, chose U  | 8.2% | 0.0% | 0.0% | 0.0% | 0.0% | 1.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.79% | -0.0 | 3.4895 | 81% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **51.2%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **81.3%** |
| **Partly employed**  | **2.5%** | **2.6%** | **4.9%** | **4.9%** | **4.9%** | **4.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 2.5% | 2.6% | 4.9% | 4.9% | 4.9% | 4.0% |
| **Unemployed**  | **46.3%** | **8.6%** | **6.3%** | **6.3%** | **6.3%** | **14.8%** |
| Offered e, chose U  | 37.6% | 0.0% | 0.0% | 0.0% | 0.0% | 7.5% |
| Offered p, chose U  | 2.4% | 2.3% | 0.0% | 0.0% | 0.0% | 0.9% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.79% | 115.18 | 3.6368 | 55% | 20% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **8.1%** | **88.8%** | **88.8%** | **88.8%** | **54.9%** |
| **Partly employed**  | **17.9%** | **69.0%** | **4.9%** | **4.9%** | **4.9%** | **20.3%** |
| Offered e, chose P  | 12.9% | 64.1% | 0.0% | 0.0% | 0.0% | 15.4% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **82.1%** | **22.9%** | **6.3%** | **6.3%** | **6.3%** | **24.8%** |
| Offered e, chose U  | 75.8% | 16.6% | 0.0% | 0.0% | 0.0% | 18.5% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 5.41% | -0.0 | 4.0077 | 64% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **23.2%** | **44.6%** | **72.2%** | **88.8%** | **88.8%** | **63.5%** |
| **Partly employed**  | **1.0%** | **2.1%** | **2.4%** | **4.1%** | **4.9%** | **2.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.0% | 2.1% | 2.4% | 4.1% | 4.9% | 2.9% |
| **Unemployed**  | **75.9%** | **53.3%** | **25.3%** | **7.1%** | **6.3%** | **33.6%** |
| Offered e, chose U  | 65.6% | 44.2% | 16.5% | 0.0% | 0.0% | 25.3% |
| Offered p, chose U  | 3.9% | 2.8% | 2.5% | 0.8% | 0.0% | 2.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 5.41% | 132.9 | 4.2099 | 43% | 10% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **35.2%** | **88.8%** | **88.8%** | **42.6%** |
| **Partly employed**  | **9.4%** | **25.4%** | **4.9%** | **4.9%** | **4.9%** | **9.9%** |
| Offered e, chose P  | 4.5% | 20.4% | 0.0% | 0.0% | 0.0% | 5.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **90.6%** | **74.6%** | **59.9%** | **6.3%** | **6.3%** | **47.6%** |
| Offered e, chose U  | 84.3% | 68.3% | 53.6% | 0.0% | 0.0% | 41.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 2.5 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 97.46 | 2.5896 | 72% | 22% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **5.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **72.2%** |
| **Partly employed**  | **87.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **21.5%** |
| Offered e, chose P  | 83.0% | 0.0% | 0.0% | 0.0% | 0.0% | 16.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.4% | -0.0 | 2.9936 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **2.2%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.4%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 2.2% | 4.9% | 4.9% | 4.9% | 4.9% | 4.4% |
| **Unemployed**  | **9.0%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.9%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 2.7% | 0.0% | 0.0% | 0.0% | 0.0% | 0.5% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.4% | 132.9 | 3.1211 | 59% | 20% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **28.0%** | **88.8%** | **88.8%** | **88.8%** | **58.9%** |
| **Partly employed**  | **21.0%** | **64.3%** | **4.9%** | **4.9%** | **4.9%** | **20.0%** |
| Offered e, chose P  | 16.1% | 59.4% | 0.0% | 0.0% | 0.0% | 15.1% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **79.0%** | **7.7%** | **6.3%** | **6.3%** | **6.3%** | **21.1%** |
| Offered e, chose U  | 72.7% | 1.3% | 0.0% | 0.0% | 0.0% | 14.8% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 4.41% | 0.0 | 3.488 | 77% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **41.9%** | **78.8%** | **88.8%** | **88.8%** | **88.8%** | **77.4%** |
| **Partly employed**  | **1.4%** | **1.3%** | **2.3%** | **4.9%** | **4.9%** | **3.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.4% | 1.3% | 2.3% | 4.9% | 4.9% | 3.0% |
| **Unemployed**  | **56.7%** | **20.0%** | **8.9%** | **6.3%** | **6.3%** | **19.6%** |
| Offered e, chose U  | 46.9% | 10.0% | 0.0% | 0.0% | 0.0% | 11.4% |
| Offered p, chose U  | 3.5% | 3.6% | 2.6% | 0.0% | 0.0% | 1.9% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 4.41% | 168.34 | 3.6882 | 45% | 8% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **49.4%** | **88.8%** | **88.8%** | **45.4%** |
| **Partly employed**  | **8.6%** | **18.2%** | **4.9%** | **4.9%** | **4.9%** | **8.3%** |
| Offered e, chose P  | 3.7% | 13.3% | 0.0% | 0.0% | 0.0% | 3.4% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **91.4%** | **81.8%** | **45.6%** | **6.3%** | **6.3%** | **46.3%** |
| Offered e, chose U  | 85.1% | 75.5% | 39.3% | 0.0% | 0.0% | 40.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 7.27% | -0.0 | 4.0082 | 57% | 2% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **13.7%** | **34.7%** | **60.7%** | **88.8%** | **88.8%** | **57.3%** |
| **Partly employed**  | **0.2%** | **1.1%** | **1.1%** | **1.5%** | **4.9%** | **1.8%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.2% | 1.1% | 1.1% | 1.5% | 4.9% | 1.8% |
| **Unemployed**  | **86.0%** | **64.2%** | **38.2%** | **9.7%** | **6.3%** | **40.9%** |
| Offered e, chose U  | 75.1% | 54.1% | 28.1% | 0.0% | 0.0% | 31.4% |
| Offered p, chose U  | 4.7% | 3.8% | 3.8% | 3.4% | 0.0% | 3.1% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 7.27% | 212.64 | 4.2796 | 29% | 6% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **8.6%** | **48.3%** | **88.8%** | **29.1%** |
| **Partly employed**  | **5.8%** | **9.3%** | **4.9%** | **4.9%** | **4.9%** | **6.0%** |
| Offered e, chose P  | 0.9% | 4.4% | 0.0% | 0.0% | 0.0% | 1.1% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.2%** | **90.7%** | **86.4%** | **46.8%** | **6.3%** | **64.9%** |
| Offered e, chose U  | 87.9% | 84.4% | 80.1% | 40.5% | 0.0% | 58.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.42% | -0.0 | 2.4996 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **2.1%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 2.1% | 4.9% | 4.9% | 4.9% | 4.9% | 4.3% |
| **Unemployed**  | **9.2%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.9%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 2.9% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.42% | 194.92 | 2.6348 | 55% | 15% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **6.7%** | **88.8%** | **88.8%** | **88.8%** | **54.6%** |
| **Partly employed**  | **11.6%** | **46.6%** | **4.9%** | **4.9%** | **4.9%** | **14.6%** |
| Offered e, chose P  | 6.6% | 41.7% | 0.0% | 0.0% | 0.0% | 9.7% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **88.4%** | **46.8%** | **6.3%** | **6.3%** | **6.3%** | **30.8%** |
| Offered e, chose U  | 82.1% | 40.5% | 0.0% | 0.0% | 0.0% | 24.5% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 4.12% | 0.0 | 2.9885 | 88% | 2% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **84.7%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.0%** |
| **Partly employed**  | **0.5%** | **0.7%** | **1.1%** | **1.6%** | **4.2%** | **1.6%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.5% | 0.7% | 1.1% | 1.6% | 4.2% | 1.6% |
| **Unemployed**  | **14.8%** | **10.5%** | **10.1%** | **9.6%** | **7.0%** | **10.4%** |
| Offered e, chose U  | 4.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.8% |
| Offered p, chose U  | 4.4% | 4.2% | 3.8% | 3.3% | 0.7% | 3.3% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 4.12% | 274.66 | 3.2141 | 40% | 6% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **24.0%** | **88.8%** | **88.8%** | **40.3%** |
| **Partly employed**  | **6.2%** | **7.7%** | **4.9%** | **4.9%** | **4.9%** | **5.7%** |
| Offered e, chose P  | 1.3% | 2.8% | 0.0% | 0.0% | 0.0% | 0.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **93.8%** | **92.3%** | **71.1%** | **6.3%** | **6.3%** | **54.0%** |
| Offered e, chose U  | 87.5% | 86.0% | 64.8% | 0.0% | 0.0% | 47.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 7.48% | 0.0 | 3.4773 | 67% | 1% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **19.5%** | **49.8%** | **87.6%** | **88.8%** | **88.8%** | **66.9%** |
| **Partly employed**  | **0.3%** | **0.4%** | **0.5%** | **0.7%** | **1.3%** | **0.6%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.3% | 0.4% | 0.5% | 0.7% | 1.3% | 0.6% |
| **Unemployed**  | **80.3%** | **49.8%** | **11.9%** | **10.6%** | **10.0%** | **32.5%** |
| Offered e, chose U  | 69.3% | 39.0% | 1.1% | 0.0% | 0.0% | 21.9% |
| Offered p, chose U  | 4.7% | 4.6% | 4.5% | 4.3% | 3.7% | 4.3% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 7.48% | 345.54 | 3.8099 | 24% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **1.3%** | **30.3%** | **88.8%** | **24.1%** |
| **Partly employed**  | **5.3%** | **5.6%** | **4.9%** | **4.9%** | **4.9%** | **5.1%** |
| Offered e, chose P  | 0.3% | 0.7% | 0.0% | 0.0% | 0.0% | 0.2% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.7%** | **94.4%** | **93.8%** | **64.8%** | **6.3%** | **70.8%** |
| Offered e, chose U  | 88.4% | 88.1% | 87.5% | 58.5% | 0.0% | 64.5% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 17.55% | -0.0 | 3.9709 | 37% | 0% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **1.4%** | **9.7%** | **30.2%** | **56.5%** | **88.8%** | **37.3%** |
| **Partly employed**  | **0.0%** | **0.1%** | **0.2%** | **0.4%** | **0.6%** | **0.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.0% | 0.1% | 0.2% | 0.4% | 0.6% | 0.3% |
| **Unemployed**  | **98.6%** | **90.1%** | **69.5%** | **43.1%** | **10.6%** | **62.4%** |
| Offered e, chose U  | 87.4% | 79.1% | 58.5% | 32.3% | 0.0% | 51.5% |
| Offered p, chose U  | 4.9% | 4.8% | 4.7% | 4.5% | 4.3% | 4.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 17.55% | 327.82 | 4.3722 | 15% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **0.0%** | **2.1%** | **73.3%** | **15.1%** |
| **Partly employed**  | **5.1%** | **5.2%** | **5.5%** | **4.9%** | **4.9%** | **5.1%** |
| Offered e, chose P  | 0.2% | 0.3% | 0.6% | 0.0% | 0.0% | 0.2% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.9%** | **94.8%** | **94.5%** | **93.0%** | **21.8%** | **79.8%** |
| Offered e, chose U  | 88.6% | 88.5% | 88.2% | 86.7% | 15.4% | 73.5% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 3.4262 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 62.02 | 3.5076 | 88% | 6% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **85.9%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.2%** |
| **Partly employed**  | **7.8%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **5.5%** |
| Offered e, chose P  | 2.9% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.846 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 4.9561 | 68% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **74.2%** | **88.8%** | **88.8%** | **88.8%** | **68.1%** |
| **Partly employed**  | **79.7%** | **19.5%** | **4.9%** | **4.9%** | **4.9%** | **22.8%** |
| Offered e, chose P  | 74.8% | 14.6% | 0.0% | 0.0% | 0.0% | 17.9% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **20.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **9.1%** |
| Offered e, chose U  | 14.0% | 0.0% | 0.0% | 0.0% | 0.0% | 2.8% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 4.24% | -0.0 | 6.2726 | 75% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **40.3%** | **67.0%** | **88.8%** | **88.8%** | **88.8%** | **74.7%** |
| **Partly employed**  | **3.0%** | **3.4%** | **4.9%** | **4.9%** | **4.9%** | **4.2%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 3.0% | 3.4% | 4.9% | 4.9% | 4.9% | 4.2% |
| **Unemployed**  | **56.7%** | **29.6%** | **6.3%** | **6.3%** | **6.3%** | **21.0%** |
| Offered e, chose U  | 48.5% | 21.7% | 0.0% | 0.0% | 0.0% | 14.0% |
| Offered p, chose U  | 1.9% | 1.5% | 0.0% | 0.0% | 0.0% | 0.7% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 4.24% | 124.04 | 6.4434 | 45% | 29% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **48.7%** | **88.8%** | **88.8%** | **45.2%** |
| **Partly employed**  | **16.6%** | **71.6%** | **45.0%** | **4.9%** | **4.9%** | **28.6%** |
| Offered e, chose P  | 11.7% | 66.7% | 40.1% | 0.0% | 0.0% | 23.7% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **83.4%** | **28.4%** | **6.3%** | **6.3%** | **6.3%** | **26.1%** |
| Offered e, chose U  | 77.1% | 22.1% | 0.0% | 0.0% | 0.0% | 19.8% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.5, γl=0.5, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 6.58% | -0.0 | 7.7361 | 55% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **15.8%** | **32.7%** | **53.6%** | **83.5%** | **88.8%** | **54.9%** |
| **Partly employed**  | **0.8%** | **2.0%** | **3.2%** | **3.7%** | **4.9%** | **2.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.8% | 2.0% | 3.2% | 3.7% | 4.9% | 2.9% |
| **Unemployed**  | **83.4%** | **65.4%** | **43.2%** | **12.9%** | **6.3%** | **42.2%** |
| Offered e, chose U  | 73.0% | 56.1% | 35.1% | 5.3% | 0.0% | 33.9% |
| Offered p, chose U  | 4.1% | 3.0% | 1.8% | 1.3% | 0.0% | 2.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.5, γl=0.5, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 6.58% | 141.76 | 7.9669 | 27% | 30% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **0.0%** | **46.4%** | **88.8%** | **27.0%** |
| **Partly employed**  | **8.1%** | **22.5%** | **71.5%** | **44.8%** | **4.9%** | **30.3%** |
| Offered e, chose P  | 3.2% | 17.5% | 66.6% | 39.9% | 0.0% | 25.4% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **91.9%** | **77.5%** | **28.5%** | **8.8%** | **6.3%** | **42.6%** |
| Offered e, chose U  | 85.6% | 71.2% | 22.2% | 2.5% | 0.0% | 36.3% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 3.4262 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 97.46 | 3.5205 | 71% | 22% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **2.2%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.5%** |
| **Partly employed**  | **91.5%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **22.2%** |
| Offered e, chose P  | 86.6% | 0.0% | 0.0% | 0.0% | 0.0% | 17.3% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.41% | -0.0 | 4.8459 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **1.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.3% |
| **Unemployed**  | **9.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.9%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 3.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.41% | 141.76 | 4.9925 | 54% | 24% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **5.0%** | **88.8%** | **88.8%** | **88.8%** | **54.3%** |
| **Partly employed**  | **18.8%** | **85.7%** | **4.9%** | **4.9%** | **4.9%** | **23.9%** |
| Offered e, chose P  | 13.9% | 80.8% | 0.0% | 0.0% | 0.0% | 19.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **81.2%** | **9.3%** | **6.3%** | **6.3%** | **6.3%** | **21.9%** |
| Offered e, chose U  | 74.8% | 2.9% | 0.0% | 0.0% | 0.0% | 15.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 5.12% | -0.0 | 6.2725 | 70% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **28.5%** | **56.5%** | **88.8%** | **88.8%** | **88.8%** | **70.3%** |
| **Partly employed**  | **1.2%** | **1.9%** | **2.1%** | **4.9%** | **4.9%** | **3.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.2% | 1.9% | 2.1% | 4.9% | 4.9% | 3.0% |
| **Unemployed**  | **70.4%** | **41.6%** | **9.1%** | **6.3%** | **6.3%** | **26.7%** |
| Offered e, chose U  | 60.3% | 32.2% | 0.0% | 0.0% | 0.0% | 18.5% |
| Offered p, chose U  | 3.7% | 3.0% | 2.8% | 0.0% | 0.0% | 1.9% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 5.12% | 177.20000000000002 | 6.5002 | 40% | 10% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **23.5%** | **88.8%** | **88.8%** | **40.2%** |
| **Partly employed**  | **7.9%** | **16.3%** | **16.9%** | **4.9%** | **4.9%** | **10.2%** |
| Offered e, chose P  | 3.0% | 11.4% | 12.0% | 0.0% | 0.0% | 5.3% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **92.1%** | **83.7%** | **59.6%** | **6.3%** | **6.3%** | **49.6%** |
| Offered e, chose U  | 85.8% | 77.4% | 53.3% | 0.0% | 0.0% | 43.3% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.5, γl=0.5, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 10.04% | 0.0 | 7.7313 | 46% | 2% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **6.6%** | **22.1%** | **42.5%** | **69.5%** | **88.8%** | **45.9%** |
| **Partly employed**  | **0.3%** | **0.8%** | **1.8%** | **1.7%** | **4.4%** | **1.8%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.3% | 0.8% | 1.8% | 1.7% | 4.4% | 1.8% |
| **Unemployed**  | **93.1%** | **77.2%** | **55.7%** | **28.8%** | **6.9%** | **52.3%** |
| Offered e, chose U  | 82.2% | 66.7% | 46.3% | 19.3% | 0.0% | 42.9% |
| Offered p, chose U  | 4.7% | 4.1% | 3.1% | 3.2% | 0.6% | 3.1% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.5, γl=0.5, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 10.04% | 212.64 | 8.0327 | 23% | 8% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **0.0%** | **27.3%** | **88.8%** | **23.2%** |
| **Partly employed**  | **5.8%** | **8.6%** | **16.8%** | **4.9%** | **4.9%** | **8.2%** |
| Offered e, chose P  | 0.9% | 3.7% | 11.9% | 0.0% | 0.0% | 3.3% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.2%** | **91.4%** | **83.2%** | **67.7%** | **6.3%** | **68.6%** |
| Offered e, chose U  | 87.9% | 85.1% | 76.9% | 61.4% | 0.0% | 62.3% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.47% | -0.0 | 3.4254 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **1.8%** | **3.6%** | **4.9%** | **4.9%** | **4.9%** | **4.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.8% | 3.6% | 4.9% | 4.9% | 4.9% | 4.0% |
| **Unemployed**  | **9.4%** | **7.6%** | **6.3%** | **6.3%** | **6.3%** | **7.2%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 3.1% | 1.3% | 0.0% | 0.0% | 0.0% | 0.9% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.47% | 203.78 | 3.5706 | 54% | 14% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **2.0%** | **88.8%** | **88.8%** | **88.8%** | **53.7%** |
| **Partly employed**  | **11.1%** | **42.2%** | **4.9%** | **4.9%** | **4.9%** | **13.6%** |
| Offered e, chose P  | 6.2% | 37.3% | 0.0% | 0.0% | 0.0% | 8.7% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **88.9%** | **55.8%** | **6.3%** | **6.3%** | **6.3%** | **32.7%** |
| Offered e, chose U  | 82.6% | 49.5% | 0.0% | 0.0% | 0.0% | 26.4% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 4.71% | -0.0 | 4.8365 | 83% | 1% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **60.9%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **83.2%** |
| **Partly employed**  | **0.6%** | **0.7%** | **1.0%** | **1.5%** | **3.5%** | **1.5%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.6% | 0.7% | 1.0% | 1.5% | 3.5% | 1.5% |
| **Unemployed**  | **38.6%** | **10.6%** | **10.2%** | **9.7%** | **7.7%** | **15.4%** |
| Offered e, chose U  | 27.9% | 0.0% | 0.0% | 0.0% | 0.0% | 5.6% |
| Offered p, chose U  | 4.4% | 4.2% | 3.9% | 3.4% | 1.4% | 3.5% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 4.71% | 283.52 | 5.0904 | 37% | 6% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **8.0%** | **88.8%** | **88.8%** | **37.1%** |
| **Partly employed**  | **6.1%** | **7.5%** | **4.9%** | **4.9%** | **4.9%** | **5.7%** |
| Offered e, chose P  | 1.2% | 2.6% | 0.0% | 0.0% | 0.0% | 0.7% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **93.9%** | **92.5%** | **87.1%** | **6.3%** | **6.3%** | **57.2%** |
| Offered e, chose U  | 87.6% | 86.2% | 80.8% | 0.0% | 0.0% | 50.9% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 10.09% | 0.0 | 6.255 | 56% | 1% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **9.4%** | **30.5%** | **62.6%** | **88.8%** | **88.8%** | **56.0%** |
| **Partly employed**  | **0.2%** | **0.3%** | **0.5%** | **0.6%** | **1.1%** | **0.5%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.2% | 0.3% | 0.5% | 0.6% | 1.1% | 0.5% |
| **Unemployed**  | **90.5%** | **69.2%** | **36.9%** | **10.6%** | **10.1%** | **43.5%** |
| Offered e, chose U  | 79.4% | 58.3% | 26.2% | 0.0% | 0.0% | 32.8% |
| Offered p, chose U  | 4.8% | 4.6% | 4.4% | 4.3% | 3.8% | 4.4% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 10.09% | 345.54 | 6.6221 | 20% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **0.0%** | **10.7%** | **88.8%** | **19.9%** |
| **Partly employed**  | **5.2%** | **5.5%** | **6.6%** | **4.9%** | **4.9%** | **5.4%** |
| Offered e, chose P  | 0.3% | 0.6% | 1.7% | 0.0% | 0.0% | 0.5% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.8%** | **94.5%** | **93.4%** | **84.3%** | **6.3%** | **74.7%** |
| Offered e, chose U  | 88.5% | 88.1% | 87.1% | 78.0% | 0.0% | 68.3% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.5, γl=0.5, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 25.62% | 0.0 | 7.6728 | 26% | 0% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.3%** | **2.5%** | **12.1%** | **30.5%** | **82.4%** | **25.5%** |
| **Partly employed**  | **0.0%** | **0.0%** | **0.2%** | **0.3%** | **0.5%** | **0.2%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.0% | 0.0% | 0.2% | 0.3% | 0.5% | 0.2% |
| **Unemployed**  | **99.7%** | **97.5%** | **87.8%** | **69.2%** | **17.1%** | **74.3%** |
| Offered e, chose U  | 88.5% | 86.3% | 76.7% | 58.3% | 6.4% | 63.2% |
| Offered p, chose U  | 4.9% | 4.9% | 4.8% | 4.6% | 4.4% | 4.7% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.5, γl=0.5, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 25.62% | 354.40000000000003 | 8.087 | 7% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **0.0%** | **0.7%** | **36.5%** | **7.4%** |
| **Partly employed**  | **5.1%** | **5.1%** | **5.4%** | **4.9%** | **4.9%** | **5.1%** |
| Offered e, chose P  | 0.1% | 0.2% | 0.4% | 0.0% | 0.0% | 0.2% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.9%** | **94.9%** | **94.6%** | **94.4%** | **58.6%** | **87.5%** |
| Offered e, chose U  | 88.6% | 88.6% | 88.3% | 88.1% | 52.3% | 81.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.2098 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 62.02 | 4.3924 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.9766 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 62.02 | 5.1592 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 5.7433 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 5.9432 | 72% | 22% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **5.1%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **72.0%** |
| **Partly employed**  | **88.6%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **21.7%** |
| Offered e, chose P  | 83.7% | 0.0% | 0.0% | 0.0% | 0.0% | 16.7% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 6.5101 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 6.7426 | 71% | 17% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **66.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **17.3%** |
| Offered e, chose P  | 62.0% | 0.0% | 0.0% | 0.0% | 0.0% | 12.4% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **33.1%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **11.7%** |
| Offered e, chose U  | 26.8% | 0.0% | 0.0% | 0.0% | 0.0% | 5.4% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.2098 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 62.02 | 4.3924 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.9766 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 97.46 | 5.1814 | 71% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **93.7%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **22.7%** |
| Offered e, chose P  | 88.8% | 0.0% | 0.0% | 0.0% | 0.0% | 17.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 5.7433 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 97.46 | 5.9806 | 71% | 17% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **65.7%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **17.1%** |
| Offered e, chose P  | 60.8% | 0.0% | 0.0% | 0.0% | 0.0% | 12.2% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **34.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **11.9%** |
| Offered e, chose U  | 28.0% | 0.0% | 0.0% | 0.0% | 0.0% | 5.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.41% | -0.0 | 6.5097 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **1.8%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.8% | 4.9% | 4.9% | 4.9% | 4.9% | 4.3% |
| **Unemployed**  | **9.5%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.9%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 3.1% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.41% | 132.9 | 6.8016 | 56% | 22% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **12.8%** | **88.8%** | **88.8%** | **88.8%** | **55.8%** |
| **Partly employed**  | **13.7%** | **80.8%** | **4.9%** | **4.9%** | **4.9%** | **21.9%** |
| Offered e, chose P  | 8.8% | 75.9% | 0.0% | 0.0% | 0.0% | 16.9% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **86.3%** | **6.4%** | **6.3%** | **6.3%** | **6.3%** | **22.3%** |
| Offered e, chose U  | 79.9% | 0.1% | 0.0% | 0.0% | 0.0% | 16.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.2098 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.37% | 115.18 | 4.452 | 71% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **93.7%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **22.7%** |
| Offered e, chose P  | 88.8% | 0.0% | 0.0% | 0.0% | 0.0% | 17.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.43% | -0.0 | 4.9755 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **1.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.3% |
| **Unemployed**  | **9.4%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.9%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 3.1% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.43% | 194.92 | 5.2724 | 53% | 17% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **53.3%** |
| **Partly employed**  | **9.9%** | **59.8%** | **4.9%** | **4.9%** | **4.9%** | **16.9%** |
| Offered e, chose P  | 5.0% | 54.9% | 0.0% | 0.0% | 0.0% | 12.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **90.1%** | **40.2%** | **6.3%** | **6.3%** | **6.3%** | **29.8%** |
| Offered e, chose U  | 83.8% | 33.9% | 0.0% | 0.0% | 0.0% | 23.5% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.63% | -0.0 | 5.7387 | 89% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **0.5%** | **1.5%** | **3.1%** | **4.9%** | **4.9%** | **3.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.5% | 1.5% | 3.1% | 4.9% | 4.9% | 3.0% |
| **Unemployed**  | **10.7%** | **9.7%** | **8.2%** | **6.3%** | **6.3%** | **8.2%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 4.4% | 3.4% | 1.8% | 0.0% | 0.0% | 1.9% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.63% | 212.64 | 6.1244 | 53% | 6% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **53.3%** |
| **Partly employed**  | **6.5%** | **10.0%** | **4.9%** | **4.9%** | **4.9%** | **6.3%** |
| Offered e, chose P  | 1.6% | 5.1% | 0.0% | 0.0% | 0.0% | 1.3% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **93.5%** | **90.0%** | **6.3%** | **6.3%** | **6.3%** | **40.5%** |
| Offered e, chose U  | 87.2% | 83.7% | 0.0% | 0.0% | 0.0% | 34.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 4.63% | 0.0 | 6.4869 | 82% | 2% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **52.4%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **81.5%** |
| **Partly employed**  | **0.0%** | **0.6%** | **1.5%** | **2.8%** | **4.9%** | **2.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.0% | 0.6% | 1.5% | 2.8% | 4.9% | 2.0% |
| **Unemployed**  | **47.6%** | **10.6%** | **9.7%** | **8.4%** | **6.3%** | **16.5%** |
| Offered e, chose U  | 36.3% | 0.0% | 0.0% | 0.0% | 0.0% | 7.3% |
| Offered p, chose U  | 4.9% | 4.3% | 3.4% | 2.1% | 0.0% | 3.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 4.63% | 265.8 | 6.9644 | 41% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **28.9%** | **88.8%** | **88.8%** | **41.3%** |
| **Partly employed**  | **5.4%** | **6.3%** | **4.9%** | **4.9%** | **4.9%** | **5.3%** |
| Offered e, chose P  | 0.5% | 1.4% | 0.0% | 0.0% | 0.0% | 0.4% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.6%** | **93.7%** | **66.1%** | **6.3%** | **6.3%** | **53.4%** |
| Offered e, chose U  | 88.3% | 87.4% | 59.8% | 0.0% | 0.0% | 47.1% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 3.9367 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 62.02 | 4.1193 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.4303 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 62.02 | 4.6129 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.924 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 5.1172 | 73% | 20% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **12.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **73.4%** |
| **Partly employed**  | **81.7%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **20.3%** |
| Offered e, chose P  | 76.8% | 0.0% | 0.0% | 0.0% | 0.0% | 15.4% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 5.4177 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 5.6408 | 71% | 19% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **72.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **18.5%** |
| Offered e, chose P  | 68.0% | 0.0% | 0.0% | 0.0% | 0.0% | 13.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **27.1%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **10.5%** |
| Offered e, chose U  | 20.8% | 0.0% | 0.0% | 0.0% | 0.0% | 4.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 3.9367 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 62.02 | 4.1193 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.4303 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 97.46 | 4.6306 | 71% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **93.7%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **22.7%** |
| Offered e, chose P  | 88.8% | 0.0% | 0.0% | 0.0% | 0.0% | 17.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.924 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 97.46 | 5.1543 | 71% | 18% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **72.6%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **18.5%** |
| Offered e, chose P  | 67.7% | 0.0% | 0.0% | 0.0% | 0.0% | 13.5% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **27.4%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **10.5%** |
| Offered e, chose U  | 21.1% | 0.0% | 0.0% | 0.0% | 0.0% | 4.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.41% | -0.0 | 5.4173 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **1.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.3% |
| **Unemployed**  | **9.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.9%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 3.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.41% | 124.04 | 5.6915 | 60% | 18% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **32.1%** | **88.8%** | **88.8%** | **88.8%** | **59.7%** |
| **Partly employed**  | **15.1%** | **61.6%** | **4.9%** | **4.9%** | **4.9%** | **18.3%** |
| Offered e, chose P  | 10.2% | 56.7% | 0.0% | 0.0% | 0.0% | 13.4% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **84.9%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **22.0%** |
| Offered e, chose U  | 78.6% | 0.0% | 0.0% | 0.0% | 0.0% | 15.7% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.37% | -0.0 | 3.9367 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.37% | 115.18 | 4.1766 | 71% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **93.7%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **22.7%** |
| Offered e, chose P  | 88.8% | 0.0% | 0.0% | 0.0% | 0.0% | 17.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.43% | -0.0 | 4.4292 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **1.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.3% |
| **Unemployed**  | **9.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.9%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 3.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.43% | 194.92 | 4.7165 | 55% | 16% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **7.7%** | **88.8%** | **88.8%** | **88.8%** | **54.8%** |
| **Partly employed**  | **10.1%** | **55.7%** | **4.9%** | **4.9%** | **4.9%** | **16.1%** |
| Offered e, chose P  | 5.2% | 50.8% | 0.0% | 0.0% | 0.0% | 11.2% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **89.9%** | **36.6%** | **6.3%** | **6.3%** | **6.3%** | **29.1%** |
| Offered e, chose U  | 83.5% | 30.3% | 0.0% | 0.0% | 0.0% | 22.8% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.63% | -0.0 | 4.9195 | 89% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **0.5%** | **1.5%** | **3.3%** | **4.9%** | **4.9%** | **3.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.5% | 1.5% | 3.3% | 4.9% | 4.9% | 3.0% |
| **Unemployed**  | **10.7%** | **9.7%** | **8.0%** | **6.3%** | **6.3%** | **8.2%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 4.4% | 3.4% | 1.7% | 0.0% | 0.0% | 1.9% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.63% | 212.64 | 5.2903 | 53% | 6% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **53.3%** |
| **Partly employed**  | **6.6%** | **10.2%** | **4.9%** | **4.9%** | **4.9%** | **6.3%** |
| Offered e, chose P  | 1.7% | 5.3% | 0.0% | 0.0% | 0.0% | 1.4% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **93.4%** | **89.8%** | **6.3%** | **6.3%** | **6.3%** | **40.4%** |
| Offered e, chose U  | 87.0% | 83.4% | 0.0% | 0.0% | 0.0% | 34.1% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 4.2% | -0.0 | 5.4019 | 85% | 2% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **72.3%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **85.5%** |
| **Partly employed**  | **0.0%** | **0.6%** | **1.5%** | **3.0%** | **4.9%** | **2.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.0% | 0.6% | 1.5% | 3.0% | 4.9% | 2.0% |
| **Unemployed**  | **27.7%** | **10.6%** | **9.7%** | **8.2%** | **6.3%** | **12.5%** |
| Offered e, chose U  | 16.4% | 0.0% | 0.0% | 0.0% | 0.0% | 3.3% |
| Offered p, chose U  | 4.9% | 4.3% | 3.4% | 1.9% | 0.0% | 2.9% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 4.2% | 239.22000000000003 | 5.857 | 48% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **61.1%** | **88.8%** | **88.8%** | **47.7%** |
| **Partly employed**  | **5.4%** | **7.3%** | **4.9%** | **4.9%** | **4.9%** | **5.5%** |
| Offered e, chose P  | 0.5% | 2.4% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.6%** | **92.7%** | **34.0%** | **6.3%** | **6.3%** | **46.8%** |
| Offered e, chose U  | 88.3% | 86.4% | 27.7% | 0.0% | 0.0% | 40.5% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.8628 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 62.02 | 5.0454 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 6.2827 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 62.02 | 6.4653 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **87.7%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.6%** |
| **Partly employed**  | **6.0%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **5.1%** |
| Offered e, chose P  | 1.1% | 0.0% | 0.0% | 0.0% | 0.0% | 0.2% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 7.7025 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 7.9098 | 71% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **93.7%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **22.7%** |
| Offered e, chose P  | 88.8% | 0.0% | 0.0% | 0.0% | 0.0% | 17.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.3, γl=0.3, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 9.1223 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.3, γl=0.3, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 9.3651 | 70% | 17% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **85.3%** | **88.8%** | **88.8%** | **88.8%** | **70.3%** |
| **Partly employed**  | **60.9%** | **8.4%** | **4.9%** | **4.9%** | **4.9%** | **16.8%** |
| Offered e, chose P  | 55.9% | 3.4% | 0.0% | 0.0% | 0.0% | 11.9% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **39.1%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **12.9%** |
| Offered e, chose U  | 32.8% | 0.0% | 0.0% | 0.0% | 0.0% | 6.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.8628 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 62.02 | 5.0454 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 6.2827 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 97.46 | 6.4924 | 71% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **93.7%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **22.7%** |
| Offered e, chose P  | 88.8% | 0.0% | 0.0% | 0.0% | 0.0% | 17.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.37% | -0.0 | 7.7025 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.37% | 97.46 | 7.9475 | 71% | 16% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.7%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **59.6%** | **5.0%** | **4.9%** | **4.9%** | **4.9%** | **15.9%** |
| Offered e, chose P  | 54.7% | 0.1% | 0.0% | 0.0% | 0.0% | 11.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **40.4%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **13.1%** |
| Offered e, chose U  | 34.0% | 0.0% | 0.0% | 0.0% | 0.0% | 6.8% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.3, γl=0.3, π=0.3

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 0 | 3.55% | -0.0 | 9.1188 | 87% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **78.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **86.6%** |
| **Partly employed**  | **1.8%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.8% | 4.9% | 4.9% | 4.9% | 4.9% | 4.3% |
| **Unemployed**  | **20.2%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **9.1%** |
| Offered e, chose U  | 10.8% | 0.0% | 0.0% | 0.0% | 0.0% | 2.2% |
| Offered p, chose U  | 3.1% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.3, γl=0.3, π=0.3

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 15 | 0.5 | 600 | 3.55% | 132.9 | 9.4307 | 54% | 24% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **3.1%** | **88.8%** | **88.8%** | **88.8%** | **53.9%** |
| **Partly employed**  | **13.0%** | **90.2%** | **4.9%** | **4.9%** | **4.9%** | **23.6%** |
| Offered e, chose P  | 8.1% | 85.3% | 0.0% | 0.0% | 0.0% | 18.7% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **87.0%** | **6.7%** | **6.3%** | **6.3%** | **6.3%** | **22.5%** |
| Offered e, chose U  | 80.7% | 0.4% | 0.0% | 0.0% | 0.0% | 16.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.37% | -0.0 | 4.8628 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.37% | 115.18 | 5.1076 | 71% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **71.0%** |
| **Partly employed**  | **93.7%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **22.7%** |
| Offered e, chose P  | 88.8% | 0.0% | 0.0% | 0.0% | 0.0% | 17.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.43% | -0.0 | 6.2816 | 89% | 4% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **1.8%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.8% | 4.9% | 4.9% | 4.9% | 4.9% | 4.3% |
| **Unemployed**  | **9.5%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.9%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 3.2% | 0.0% | 0.0% | 0.0% | 0.0% | 0.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.43% | 194.92 | 6.5891 | 53% | 16% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **53.3%** |
| **Partly employed**  | **9.6%** | **54.0%** | **4.9%** | **4.9%** | **4.9%** | **15.7%** |
| Offered e, chose P  | 4.7% | 49.1% | 0.0% | 0.0% | 0.0% | 10.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **90.4%** | **46.0%** | **6.3%** | **6.3%** | **6.3%** | **31.1%** |
| Offered e, chose U  | 84.1% | 39.7% | 0.0% | 0.0% | 0.0% | 24.8% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1.5, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 3.64% | -0.0 | 7.6977 | 89% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **0.5%** | **1.5%** | **2.9%** | **4.9%** | **4.9%** | **2.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.5% | 1.5% | 2.9% | 4.9% | 4.9% | 2.9% |
| **Unemployed**  | **10.7%** | **9.7%** | **8.3%** | **6.3%** | **6.3%** | **8.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 4.4% | 3.4% | 2.0% | 0.0% | 0.0% | 2.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1.5, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 3.64% | 212.64 | 8.0996 | 53% | 6% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **88.8%** | **88.8%** | **88.8%** | **53.3%** |
| **Partly employed**  | **6.4%** | **9.9%** | **4.9%** | **4.9%** | **4.9%** | **6.2%** |
| Offered e, chose P  | 1.5% | 4.9% | 0.0% | 0.0% | 0.0% | 1.3% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **93.6%** | **90.1%** | **6.3%** | **6.3%** | **6.3%** | **40.5%** |
| Offered e, chose U  | 87.2% | 83.8% | 0.0% | 0.0% | 0.0% | 34.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=2, γc=0.3, γl=0.3, π=0.5

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 0 | 4.96% | -0.0 | 9.0964 | 79% | 2% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **38.0%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **78.6%** |
| **Partly employed**  | **0.0%** | **0.5%** | **1.5%** | **2.5%** | **4.9%** | **1.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 0.0% | 0.5% | 1.5% | 2.5% | 4.9% | 1.9% |
| **Unemployed**  | **62.0%** | **10.7%** | **9.7%** | **8.8%** | **6.3%** | **19.5%** |
| Offered e, chose U  | 50.7% | 0.0% | 0.0% | 0.0% | 0.0% | 10.1% |
| Offered p, chose U  | 4.9% | 4.4% | 3.4% | 2.5% | 0.0% | 3.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=2, γc=0.3, γl=0.3, π=0.5

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 15 | 0.5 | 600 | 4.96% | 283.52 | 9.5989 | 38% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **13.2%** | **88.8%** | **88.8%** | **38.2%** |
| **Partly employed**  | **5.3%** | **6.2%** | **4.9%** | **4.9%** | **4.9%** | **5.3%** |
| Offered e, chose P  | 0.4% | 1.3% | 0.0% | 0.0% | 0.0% | 0.3% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **94.7%** | **93.8%** | **81.9%** | **6.3%** | **6.3%** | **56.6%** |
| Offered e, chose U  | 88.4% | 87.5% | 75.6% | 0.0% | 0.0% | 50.3% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=0.5, γc=0.7, γl=0.7, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 3.37% | -0.0 | 2.1809 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** | **88.8%** |
| **Partly employed**  | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** | **4.9%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=0.5, γc=0.7, γl=0.7, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 3.37% | 88.60000000000001 | 2.2285 | 69% | 24% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **3.2%** | **76.5%** | **88.8%** | **88.8%** | **88.8%** | **69.2%** |
| **Partly employed**  | **85.7%** | **17.2%** | **4.9%** | **4.9%** | **4.9%** | **23.5%** |
| Offered e, chose P  | 80.8% | 12.3% | 0.0% | 0.0% | 0.0% | 18.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **11.0%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **7.3%** |
| Offered e, chose U  | 4.7% | 0.0% | 0.0% | 0.0% | 0.0% | 0.9% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---













### ψ=1, γc=0.7, γl=0.7, π=0.2

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 0 | 7.07% | -0.0 | 2.9615 | 57% | 3% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **33.8%** | **44.1%** | **54.5%** | **66.5%** | **88.0%** | **57.4%** |
| **Partly employed**  | **1.9%** | **2.5%** | **2.8%** | **2.8%** | **3.2%** | **2.7%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 1.9% | 2.5% | 2.8% | 2.8% | 3.2% | 2.7% |
| **Unemployed**  | **64.3%** | **53.4%** | **42.7%** | **30.7%** | **8.8%** | **40.0%** |
| Offered e, chose U  | 55.0% | 44.7% | 34.3% | 22.3% | 0.7% | 31.4% |
| Offered p, chose U  | 3.0% | 2.4% | 2.1% | 2.1% | 1.7% | 2.3% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### ψ=1, γc=0.7, γl=0.7, π=0.2

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 15 | 0.5 | 600 | 7.07% | 150.62 | 3.0748 | 27% | 22% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.0%** | **0.0%** | **9.3%** | **47.9%** | **78.7%** | **27.2%** |
| **Partly employed**  | **12.8%** | **31.9%** | **54.7%** | **4.9%** | **4.9%** | **21.9%** |
| Offered e, chose P  | 7.9% | 27.0% | 49.8% | 0.0% | 0.0% | 16.9% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **87.2%** | **68.1%** | **35.9%** | **47.2%** | **16.4%** | **51.0%** |
| Offered e, chose U  | 80.9% | 61.8% | 29.6% | 40.9% | 10.1% | 44.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---





