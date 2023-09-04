---
title: "Office Hours: 2023 Sept 03 (Genetic algo)"
layout: presentation_solar
---

## Summary

I implemented a genetic algorithm to search over 
transition matrices χ, and enforcement rates π,
to try matching the rates of partial and full unemployment 
seen in mid-2020.

- I am able to reasonably match the aggregate rates for E,P,U.
- But cannot match the per-quintile rates for U, even when giving the search algorithm extra degrees of freedom
    - Further, the best matches to the per-quintile U rates yield absurdly high rates for P

<!--
- The best matches for aggregate rates of full/partial/un- employment exhibit little to no heterogeneity in U across quintiles.
- The best matches for U across quintiles have a rate for P which is much too high.
- When trying to match both, the algorithm typically converges to the former case.
-->

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



<!--Plenty of degrees of freedom, so easy for search to home in on a perfect fit.-->
























---



layout: true
class: header

<h2 style="background-color: #eef;">A Match for per-quintile U</h2>


---


Moments to fit: 

May 2020 Unemployment Rates by pre-pandemic earnings quintiles, 
as estimated in 
Numbers taken from Table 1 of 
*US unemployment insurance replacement rates during the pandemic*
(Ganong,Noel,Vavra, 2020)


| Quintile | 1 | 2 | 3 | 4 | 5 |
|:--|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |
| U  | 19.9% | 12.8% | 8.0% | 6.2% | 3.8% |

---


Results of search:

$$\chi = 
\begin{bmatrix}
    \chi(e,e) & \chi(e,p) & \chi(e,u) \\
    \chi(p,e) & \chi(p,p) & \chi(p,u) \\
    \chi(u,e) & \chi(u,p) & \chi(u,u) 
\end{bmatrix} = 
\begin{bmatrix}
    0.3729 & 0.6039 & 0.0232 \\
    0.1096 & 0.8083 & 0.0821 \\
    0.4078 & 0.4216 & 0.1706
\end{bmatrix}
$$

$$\pi = 0.1962$$


---

Basic Version with no bonus:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.1962 | 0.1962 | 15 | 0.5 | 0 | 8.39% | 0.0 | -1.0056 | 18% | 74% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **18.1%** | **18.1%** | **18.1%** | **18.1%** | **18.1%** | **18.1%** |
| **Partly employed**  | **74.1%** | **74.1%** | **74.1%** | **74.1%** | **74.1%** | **74.1%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 74.1% | 74.1% | 74.1% | 74.1% | 74.1% | 74.1% |
| **Unemployed**  | **7.8%** | **7.8%** | **7.8%** | **7.8%** | **7.8%** | **7.8%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 7.8% | 7.8% | 7.8% | 7.8% | 7.8% | 7.8% |


---


Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.1962 | 0.1962 | 15 | 0.5 | 600 | 8.39% | 460.72 | -0.1481 | 11% | 78% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.4%** | **2.3%** | **18.1%** | **18.1%** | **18.1%** | **11.4%** |
| **Partly employed**  | **79.3%** | **89.9%** | **74.1%** | **74.1%** | **74.1%** | **78.3%** |
| Offered e, chose P  | 5.2% | 15.7% | 0.0% | 0.0% | 0.0% | 4.2% |
| Offered p, chose P  | 74.1% | 74.1% | 74.1% | 74.1% | 74.1% | 74.1% |
| **Unemployed**  | **20.4%** | **7.8%** | **7.8%** | **7.8%** | **7.8%** | **10.3%** |
| Offered e, chose U  | 12.5% | 0.0% | 0.0% | 0.0% | 0.0% | 2.5% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 7.8% | 7.8% | 7.8% | 7.8% | 7.8% | 7.8% |


---



Now adjust the taxes to remove the deficit when the bonus is in place:

| π0 | π1 | ĥP | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.1962 | 0.1962 | 15 | 0.5 | 600 | 55.14% | -0.0 | -0.7252 | 11% | 78% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **0.4%** | **2.3%** | **18.1%** | **18.1%** | **18.1%** | **11.4%** |
| **Partly employed**  | **79.1%** | **89.8%** | **74.1%** | **74.1%** | **74.1%** | **78.3%** |
| Offered e, chose P  | 5.0% | 15.7% | 0.0% | 0.0% | 0.0% | 4.1% |
| Offered p, chose P  | 74.1% | 74.1% | 74.1% | 74.1% | 74.1% | 74.1% |
| **Unemployed**  | **20.5%** | **7.8%** | **7.8%** | **7.8%** | **7.8%** | **10.4%** |
| Offered e, chose U  | 12.7% | 0.0% | 0.0% | 0.0% | 0.0% | 2.5% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 7.8% | 7.8% | 7.8% | 7.8% | 7.8% | 7.8% |


---

Running the genetic algorithm with tweaks --
such as an even lower number of hours for P or some fixed value for π --
yields essentially the same results:

- High U for quintile 1, as desired.
- The other 4 quintiles sharing the same U
- A rate for P which is much too high.

My Conclusion from these experiments: 
It seems implausible within the model as its constructed 
for the UI bonus to be the main driving force behind the variance in unemployment across income levels.

Therefore, if fitting the model with heterogeneity to the pandemic,
it seems that the the transition matrix χ should exogenously vary by income level.
But that introduces so many variables that identifying the effect of the PUI bonus on the intrinsic margin seems hopeless.








