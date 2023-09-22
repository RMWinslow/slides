---
title: "Workshop: 2023 Sept 22"
layout: presentation_solar
parent: PUI
---

class:middle

# Workshop Presentation, Sept 22, 2023

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

<h2 style="background-color: #ded;">Partial Unemployment Insurance in Canada</h2>


---

<img src="img/20230922/cansa.png" style="max-width:100%;">


???

- Canada Emergency Response Benefit: 2000 CAD per month. For people not covered by EI. Late March to October 2020.
- Minimum Guaranteed EI benefits. Sept 2020 to (Sept/Nov 2021). Found conflicting sources on the end date there.

<a href="https://ichef.bbci.co.uk/news/976/cpsprodpb/B6A3/production/_115055764_optimised-us_cases_deaths24oct-nc.png.webp">BBC US Covid Chart</a>    
<a href="https://ichef.bbci.co.uk/news/976/cpsprodpb/25B3/production/_114915690_canada_cases_deaths-nc.png.webp">BBC Can Covid Chart</a>    
[Canada EI, NSA](img/20230922/cansa.png)






























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
| May 2020 Unemp Rate, estimated  | 19.9% | 12.8% | 8.0% | 6.2% | 3.8% |

*From Table 1 from (Ganong, Noel, and Vavra, 2020)*

### Adding this to model:

- 5 'types' of people corresponding to these income quintiles.
- Income scaled so that 886 corresponds to y=1





































---

layout: true
class: header

<h2 style="background-color: #fee;">Calibration</h2>


---


### Calibrating χ

I set

$$\chi = 
\begin{bmatrix}
   \chi(e,e) & \chi(e,p) & \chi(e,u) \\
   \chi(p,e) & \chi(p,p) & \chi(p,u) \\
   \chi(u,e) & \chi(u,p) & \chi(u,u) 
\end{bmatrix}
=
\begin{bmatrix}
   0.94 & 0.03 & 0.03 \\
   0.57 & 0.33 & 0.10 \\
   0.40 & 0.10 & 0.50 
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

These use the same values as (Hansen, Imrohoroğlu, 1992) and :

- $\beta=0.995$ (time discount factor). Same as (Şahin et al, 2002)
- $\sigma=0.5$ 
- $\rho=2.5$ 



$$\mathbb{E} \sum_j \beta^t U(c_t,l_t) = \mathbb{E} \sum_t \beta^t \frac{(c_t^{1-\sigma}l_t^\sigma)^{1-\rho}-1}{1-\rho}$$



























---

layout: true
class: header

<h2 style="background-color: #fdd;">An Example "Experiment"</h2>

---

### With π = 0.3 

Basic Version with no bonus:

| π | θp | θu | ĥP | ĥE | bonus | $\tau$ | deficit | mean $U$ |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.667 | 0.5 | 15 | 45 | 0 | 5.04% | -0.0 | -0.5286 |

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


### With π = 0.3 

Now add the 600 dollar bonus without changing tax rate:

| π | θp | θu | ĥP | ĥE | bonus | $\tau$ | deficit | mean $U$ |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.667 | 0.5 | 15 | 45 | 600 | 5.04% | 177.20000000000002 | -0.3316 |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.4%** | **3.0%** | **39.5%** | **87.8%** | **88.8%** | **43.9%** |
| **Partly employed**  | **93.3%** | **90.7%** | **54.2%** | **5.9%** | **4.9%** | **49.8%** |
| Offered e, chose P  | 88.4% | 85.8% | 49.3% | 1.0% | 0.0% | 44.9% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### With π = 0.3 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π | θp | θu | ĥP | ĥE | bonus | $\tau$ | deficit | mean $U$ |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.667 | 0.5 | 15 | 45 | 600 | 21.75% | -0.0 | -0.4851 |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.5%** | **2.8%** | **39.3%** | **87.8%** | **88.8%** | **43.9%** |
| **Partly employed**  | **93.2%** | **90.9%** | **54.4%** | **5.9%** | **4.9%** | **49.8%** |
| Offered e, chose P  | 88.2% | 85.9% | 49.4% | 0.9% | 0.0% | 44.9% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


- With many parameters, only the first quintile has an uptick in P.
- No way to induce increased Partial claims in higher quintiles without driving E way down. 

Why?

- People only vary here in terms of income and asset levels.
- Benefits drawn iid each period.

---


What if:
- each person knows whether their employment status is enforceable (that π=0 or 1)
- 30% know that is is uneforceable (π=0), 70% that it will be perfectly enforced (π=1)

Answer: A completely different kind of broken nonsense result.




---

### 30% of people have π=1, 70% π=0

Basic Version with no bonus:

| π | θp | θu | ĥP | ĥE | bonus | $\tau$ | deficit | mean $U$ |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| mixed | 0.667 | 0.5 | 15 | 45 | 0 | 13.69% | -0.0 | -0.611 |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 |  all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **45.9%** | **56.7%** | **53.2%** | **51.3%** | **53.0%** | **66.7%** |
| **Partly employed**  | **47.8%** | **37.0%** | **40.5%** | **42.4%** | **40.7%** | **27.0%** |
| Offered e, chose P  | 42.9% | 32.1% | 35.6% | 37.5% | 35.8% | 73.5% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 9.8% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 12.6% |


---


### 30% of people have π=1, 70% π=0 

Now add the 600 dollar bonus without changing tax rate:

| π | θp | θu | ĥP | ĥE | bonus | $\tau$ | deficit | mean $U$ |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| mixed | 0.667 | 0.5 | 15 | 45 | 600 | 13.69% | 248.08 | -0.3548 |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 |  all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **44.4%** | **44.4%** | **44.4%** | **44.4%** | **44.4%** | **62.1%** |
| **Partly employed**  | **2.5%** | **2.5%** | **2.5%** | **14.6%** | **49.3%** | **10.5%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 11.4% | 44.4% | 22.3% |
| Offered p, chose P  | 2.5% | 2.5% | 2.5% | 3.2% | 4.9% | 6.2% |
| **Unemployed**  | **53.2%** | **53.2%** | **53.2%** | **41.0%** | **6.3%** | **27.3%** |
| Offered e, chose U  | 44.4% | 44.4% | 44.4% | 33.0% | 0.0% | 66.5% |
| Offered p, chose U  | 2.5% | 2.5% | 2.5% | 1.7% | 0.0% | 3.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 12.6% |


---


### 30% of people have π=1, 70% π=0 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π | θp | θu | ĥP | ĥE | bonus | $\tau$ | deficit | mean $U$ |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| mixed | 0.667 | 0.5 | 15 | 45 | 600 | 35.11% | 0.0 | -0.5985 |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 |  all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **44.4%** | **44.4%** | **44.4%** | **44.4%** | **44.4%** | **62.1%** |
| **Partly employed**  | **2.5%** | **2.5%** | **2.5%** | **18.5%** | **49.3%** | **11.0%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 15.1% | 44.4% | 23.8% |
| Offered p, chose P  | 2.5% | 2.5% | 2.5% | 3.4% | 4.9% | 6.3% |
| **Unemployed**  | **53.2%** | **53.2%** | **53.2%** | **37.1%** | **6.3%** | **26.9%** |
| Offered e, chose U  | 44.4% | 44.4% | 44.4% | 29.3% | 0.0% | 65.0% |
| Offered p, chose U  | 2.5% | 2.5% | 2.5% | 1.5% | 0.0% | 3.6% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 12.6% |







