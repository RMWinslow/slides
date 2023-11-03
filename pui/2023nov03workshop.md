---
title: "Workshop: 2023 Nov 03"
layout: presentation_solar
parent: PUI
---

class:middle

# Workshop Presentation, Nov 03, 2023

Robert Winslow

Did supplemental Unemployment Compensation discourage full-time work?


---

- During the Pandemic, large supplemental payments were given to anyone collecting even a dollar of Unemployment Insurance.
- These payments were made to the fully unemployed and to those with reduced hours.
- (Ganong et al 2022) found these programs only slightly reduced the job finding rate.
- But what about the effect on the intrinsic margin?




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
- During the pandemic, the Federal Pandemic Unemployment Compensation supplement was paid out in full to anyone collecting even a single dollar of state UI.
  - 600 dollars per week April to July, 2020
  - 300 dollars per week January to September, 2021

---

### Example: State UI Benefits in Minnesota

In Minnesota, the rule is that the benefits for a given week are determined by:

$$
benefits = \begin{cases}
WBA - \frac{earnings}{2} &\text{ if } earnings < WBA \\
0 &\text{ if } earnings \geq WBA \\
\end{cases}
$$

<img src="img/20230907/MN.png" style="max-width:38%;float:right;">

where WBA is weekly benefit amount (person-specific, fixed for entire duration of benefits spell)
and the earnings refers to the current week's labor income before taxes and transfers.

*Figure on right: earnings and benefits for a hypothetical Minnesota worker with a WBA of 477 USD*

---

### State UI Recipients Over Time, MN

<img src="img/20230505/saMNwide.png" style="max-width:100%;">










































---

layout: true
class: header

<h2 style="background-color: #eef;">Model</h2>

---

- Model of unemployment insurance with partial employment and moral hazard.
- Based on:
    - *The role of unemployment insurance in an economy with liquidity constraints and moral hazard* (Hansen, Imrohoroğlu, 1992)
    - *Unemployment insurance and the role of self-insurance.* (Abdulkadiroğlu, Kuruşçu, Şahin, 2002).
- My main contribution is the addition of *partial* unemployment insurance.


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

<!--$$\mathbb{E} \sum_j \beta^t U(c_t,l_t) = \mathbb{E} \sum_t \beta^t \Big(\frac{c_t^{1-\gamma_c}}{1-\gamma_c} + \psi \cdot \frac{l_t^{1-\gamma_l}}{1-\gamma_l}\Big)$$-->

$$\mathbb{E} \sum_j \beta^t U(c_t,l_t) = \mathbb{E} \sum_t \beta^t \frac{(c_t^{1-\sigma}l_t^\sigma)^{1-\rho}-1}{1-\rho}$$


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
   (1-\tau)y\frac{\hP}{\hE} &\text{if } (\eta,\mu)=(\etaP,0) \\
   0                        &\text{if } (\eta,\mu)=(\etaU,0) \\
   (1-\tau)yθ_p             &\text{if } (\eta,\mu)=(\etaP,1) \\
   (1-\tau)yθ_u             &\text{if } (\eta,\mu)=(\etaU,1) \\
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

<!--(Note that $yθ_p = y\frac{\hP}{\hE} + benefits$.)-->


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
- Government budget balanced (?)







---

### Adding heterogeneity to the model.

In *US unemployment insurance replacement rates during the pandemic* (Ganong, Noel, and Vavra, 2020), 
the authors use CPS data to estimate the income distribution of 
workers benefitting from the Pandemic Unemployment Compensation.

| Quintile | 1 | 2 | 3 | 4 | 5 |
|:--|:-:|:-:|:-:|:-:|:-:|
| Pre-pandemic Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |

*From Table 1 from (Ganong, Noel, and Vavra, 2020)*

<!--
| May 2020 Unemp Rate, estimated  | 19.9% | 12.8% | 8.0% | 6.2% | 3.8% |
-->

### Adding this to model:

- 5 'types' of people corresponding to these income quintiles.
- Income scaled so that 886 corresponds to y=1





































---

layout: true
class: header

<h2 style="background-color: #fee;">Calibration</h2>


---


### Calibrating χ

Each period is 1 month.

I set

$$\chi = 
\begin{bmatrix}
   \chi(e,e) & \chi(e,p) & \chi(e,u) \\
   \chi(p,e) & \chi(p,p) & \chi(p,u) \\
   \chi(u,e) & \chi(u,p) & \chi(u,u) 
\end{bmatrix}
=
\begin{bmatrix}
   0.98 & 0.01 & 0.01\\
   0.10 & 0.75 & 0.15\\
   0.20 & 0.05 & 0.75
\end{bmatrix}
$$

Which has stationary distribution $[0.89, 0.05, 0.06]$.




---

### working time

- $\hE$ is set to $0.45$, representing a full work week of 45 hours out of possible 100.
- And time spent for part-time work is set to $\hP=0.15$.

<!--- $\hE=0.45$ (time Spent for full time work.)-->


---

### Other parameters:


- $\beta=0.9966$ (time discount factor)
- $\sigma=0.5$ 
- $\rho=2.5$ 
- $\pi=0.2$ 
- $\theta_u=0.5$
- $\theta_p=0.\bar{6}$


$$\mathbb{E} \sum_j \beta^t U(c_t,l_t) = \mathbb{E} \sum_t \beta^t \frac{(c_t^{1-\sigma}l_t^\sigma)^{1-\rho}-1}{1-\rho}$$



















---

layout: true
class: header

<h2 style="background-color: #fdd;">Policy Experiments in the Model</h2>

### Comparison of Static Equilibria

---



Worker Response in Baseline Economy:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.7%** | **88.7%** | **88.7%** | **88.7%** | **88.7%** | **88.7%** |
| **Partly employed**  | **4.8%** | **4.8%** | **4.8%** | **4.8%** | **4.8%** | **4.8%** |
| &ensp;Offered E, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered P, chose P  | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% |
| **Unemployed**  | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** |
| &ensp;Offered E, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered P, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered U, chose U  | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% |


---

Now add the 600 dollar bonus without changing tax rate:


| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **6.1%** | **64.2%** | **87.9%** | **88.7%** | **88.7%** | **67.1%** |
| **Partly employed**  | **87.5%** | **29.4%** | **5.6%** | **4.8%** | **4.8%** | **26.4%** |
| &ensp;Offered E, chose P  | 82.6% | 24.5% | 0.8% | 0.0% | 0.0% | 21.6% |
| &ensp;Offered P, chose P  | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% |
| **Unemployed**  | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** |
| &ensp;Offered E, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered P, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered U, chose U  | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% |


---


Now adjust the taxes to remove the deficit when the bonus is in place:



| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **5.6%** | **63.2%** | **87.8%** | **88.7%** | **88.7%** | **66.8%** |
| **Partly employed**  | **87.9%** | **30.3%** | **5.7%** | **4.8%** | **4.8%** | **26.7%** |
| &ensp;Offered E, chose P  | 83.1% | 25.5% | 0.9% | 0.0% | 0.0% | 21.9% |
| &ensp;Offered P, chose P  | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% |
| **Unemployed**  | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** |
| &ensp;Offered E, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered P, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered U, chose U  | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% |


---

Now take the money spent on expanded UI, and instead give it per capita to everyone,
regardless of employment status. UI reverts to baseline.



| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **88.7%** | **88.7%** | **88.7%** | **88.7%** | **88.7%** | **88.7%** |
| **Partly employed**  | **4.8%** | **4.8%** | **4.8%** | **4.8%** | **4.8%** | **4.8%** |
| &ensp;Offered E, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered P, chose P  | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% |
| **Unemployed**  | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** |
| &ensp;Offered E, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered P, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered U, chose U  | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% |


---

And here give the same total amount to just the bottom two quintiles

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **55.1%** | **88.7%** | **88.7%** | **88.7%** | **88.7%** | **82.0%** |
| **Partly employed**  | **38.4%** | **4.8%** | **4.8%** | **4.8%** | **4.8%** | **11.6%** |
| &ensp;Offered E, chose P  | 33.6% | 0.0% | 0.0% | 0.0% | 0.0% | 6.7% |
| &ensp;Offered P, chose P  | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% | 4.8% |
| **Unemployed**  | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** | **6.5%** |
| &ensp;Offered E, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered P, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| &ensp;Offered U, chose U  | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% | 6.5% |




---

Comparison of these cases.

|  | τ | deficit | mean U | mean m  | $\eta=P$  | $\eta=U$ |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Baseline Stationary Equilibrium | 5.08% | -0.0 | -0.5306 | 88.71% | 4.84% | 6.45% |
| Bonus, Unbalanced Budget | 5.08% | 0.11 | -0.4057 | 67.12% | 26.43% | 6.45% |
| Bonus, Balanced Budget | 14.22% | 0.0 | -0.4889 | 66.82% | 26.72% | 6.45% |
| Per-capita transfer | 12.9% | 27.477 | -0.4734 | 88.71% | 4.84% | 6.45% |
| Bottom 40% transfer | 13.26% | 27.477 | -0.3988 | 81.99% | 11.56% | 6.45% |

---

Comparison of these cases.

Utility by Quintile

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| baseline  | -1.4151 | -0.8021 | -0.4187 | -0.1569 | 0.14 | -0.5306 |
| Bonus, Unbalanced Budget  | -1.0256 | -0.6766 | -0.3571 | -0.1226 | 0.1532 | -0.4057 |
| Bonus, Balanced Budget  | -1.153 | -0.7817 | -0.4378 | -0.1849 | 0.1127 | -0.4889 |
| Per-capita transfer  | -1.1939 | -0.7286 | -0.4027 | -0.1641 | 0.1222 | -0.4734 |
| Bottom 40% transfer  | -0.846 | -0.542 | -0.4945 | -0.2145 | 0.1032 | -0.3988 |





















---

layout: true
class: header

<h2 style="background-color: #fdd;">Policy Experiments in the Model</h2>

### Simulation of Pandemic and FPUC

---

- Start in pre-pandemic stationary equilibrium.
- Iterate measure month by month. 24 periods representing 2020 and 2021.
- Represent the direct effect of the pandemic as one time shock, where transition between months 3 and 4 is:

$$
\chi_{shock}=\begin{bmatrix}0.90 & 0.00 & 0.10\\
0.00 & 0.90 & 0.10\\
0.00 & 0.00 & 1.00
\end{bmatrix}
$$

- Then transition process reverts to normal.

---

Results (No FPUC here)

<img src="img/20231103/fpucsimnull.png" style="max-width:100%;">



---

- In addition, simulate FPUC by updating lump-sum bonus $b$ each period.
- Both the arrival and cessation of elevated benefits are unexpected.


---

Results (With FPUC Simulation)

<img src="img/20231103/fpucsim.png" style="max-width:100%;">


---



