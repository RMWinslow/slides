---
title: "Office Hours: 2023 Sept 03 (Genetic algo)"
layout: presentation_solar
---

## Summary

I implemented a genetic algorithm to search over 
transition matrices χ, and enforcement rates π,
to try matching the rates of partial and full unemployment 
seen in mid-2020.

I am able to reasonably match:
- the aggregate rates for E,P,U
- the per-quintile rates for U

But not both at the same time, even when giving the search algorithm extra degrees of freedom

- The best matches for aggregate rates of full/partial/un- employment exhibit little to no heterogeneity in U across quintiles.
- The best matches for U across quintiles have a rate for P which is much too high.


---

layout: true
class: header

<h2 style="background-color: #efe;">A match for aggregate E,P,U</h2>


---

Moments to fit: 

Aggregate equilibrium rates of E,P,U = [78%, 8%, 14%]
(when 600 dollar bonus is in place.)

Simple target chosen by eyeballing composition of CPS WKSTAT, among those at work or unemployed:

<img src="img/2023aug23/CPS IPUMS Labor Market Composition (ignoring not at work).png" style="width:100%;">



---

Results of search:

$$\chi = 
\begin{bmatrix}
    \chi(e,e) & \chi(e,p) & \chi(e,u) \\
    \chi(p,e) & \chi(p,p) & \chi(p,u) \\
    \chi(u,e) & \chi(u,p) & \chi(u,u) 
\end{bmatrix} = 
\begin{bmatrix}
    0.8701 & 0.0246 & 0.1053 \\
    0.2571 & 0.1576 & 0.5853 \\
    0.6096 & 0.2555 & 0.1349
\end{bmatrix}
$$

$$\pi = 0.0771$$



---


Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.0771 | 0.0771 | 15 | 0.5 | 0 | 7.98% | -0.0 | -0.5807 | 79% | 7% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **79.3%** | **79.3%** | **79.3%** | **79.3%** | **79.3%** | **79.3%** |
| **Partly employed**  | **6.6%** | **6.6%** | **6.6%** | **6.6%** | **6.6%** | **6.6%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 6.6% | 6.6% | 6.6% | 6.6% | 6.6% | 6.6% |
| **Unemployed**  | **14.1%** | **14.1%** | **14.1%** | **14.1%** | **14.1%** | **14.1%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 14.1% | 14.1% | 14.1% | 14.1% | 14.1% | 14.1% |


---



Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.0771 | 0.0771 | 15 | 0.5 | 600 | 7.98% | 115.18 | -0.4019 | 78% | 8% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **73.1%** | **79.3%** | **79.3%** | **79.3%** | **79.3%** | **78.0%** |
| **Partly employed**  | **12.8%** | **6.6%** | **6.6%** | **6.6%** | **6.6%** | **7.8%** |
| Offered e, chose P  | 6.2% | 0.0% | 0.0% | 0.0% | 0.0% | 1.2% |
| Offered p, chose P  | 6.6% | 6.6% | 6.6% | 6.6% | 6.6% | 6.6% |
| **Unemployed**  | **14.1%** | **14.1%** | **14.1%** | **14.1%** | **14.1%** | **14.1%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 14.1% | 14.1% | 14.1% | 14.1% | 14.1% | 14.1% |


---



Now adjust the taxes to remove the deficit when the bonus is in place:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.0771 | 0.0771 | 15 | 0.5 | 600 | 18.55% | 0.0 | -0.5043 | 78% | 8% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **73.2%** | **79.3%** | **79.3%** | **79.3%** | **79.3%** | **78.1%** |
| **Partly employed**  | **12.7%** | **6.6%** | **6.6%** | **6.6%** | **6.6%** | **7.8%** |
| Offered e, chose P  | 6.1% | 0.0% | 0.0% | 0.0% | 0.0% | 1.2% |
| Offered p, chose P  | 6.6% | 6.6% | 6.6% | 6.6% | 6.6% | 6.6% |
| **Unemployed**  | **14.1%** | **14.1%** | **14.1%** | **14.1%** | **14.1%** | **14.1%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 14.1% | 14.1% | 14.1% | 14.1% | 14.1% | 14.1% |


---




---




---

<!--Plenty of degrees of freedom, so easy for search to home in on a perfect fit.-->




The following is leftover from previous slides. Left in as testing for now:




















---



layout: true
class: header

<h2 style="background-color: #eef;">With Original Values for χ</h2>


---


Results of search:

$$\chi = 
\begin{bmatrix}
    \chi(e,e) & \chi(e,p) & \chi(e,u) \\
    \chi(p,e) & \chi(p,p) & \chi(p,u) \\
    \chi(u,e) & \chi(u,p) & \chi(u,u) 
\end{bmatrix} = 
\begin{bmatrix}
    0. & 0. & 0. \\
    0. & 0. & 0. \\
    0. & 0. & 0.
\end{bmatrix}
$$

$$\pi = 0.$$










