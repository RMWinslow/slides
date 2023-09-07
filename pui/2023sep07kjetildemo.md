---
title: "Office Hours: 2023 Sept 07 (kjetil presentation)"
layout: presentation_solar
---

- 




---

---

---

---



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

<h2 style="background-color: #dfd;">A match for aggregate E,P,U</h2>


---

---

The following is leftover from previous slides. Left in as testing for now:


---

layout: true
class: header

<h2 style="background-color: #dfd;">Experiment with New Values for χ</h2>

---

For this test, I altered just the last row of χ, 
to decrease the rate at which new full-time employment is found,
and increase the persistance of unemployment.

(Changed values are bolded. See later slide for original.)

$$\chi = 
\begin{bmatrix}
    \chi(e,e) & \chi(e,p) & \chi(e,u) \\
    \chi(p,e) & \chi(p,p) & \chi(p,u) \\
    \chi(u,e) & \chi(u,p) & \chi(u,u) 
\end{bmatrix} = 
\begin{bmatrix}
    0.94 & 0.03 & 0.03 \\
    0.57 & 0.33 & 0.1 \\
    \boldsymbol{0.2} & 0.1 & \boldsymbol{0.7}
\end{bmatrix}
$$

which yields stationary distribution (with perfect enforcement) of:

| E | P | U |
|:-:|:-:|:-:|
| 84.48% | 5.31% | 10.22% |


---

### π=0.2, lower partial hours 12.0 

Basic Version with no bonus:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 0.5 | 0 | 5.61% | -0.0 | -0.5562 | 84% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **84.5%** | **84.5%** | **84.5%** | **84.5%** | **84.5%** | **84.5%** |
| **Partly employed**  | **5.3%** | **5.3%** | **5.3%** | **5.3%** | **5.3%** | **5.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% |
| **Unemployed**  | **10.2%** | **10.2%** | **10.2%** | **10.2%** | **10.2%** | **10.2%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% |


---


### π=0.2, lower partial hours 12.0 

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 0.5 | 600 | 5.61% | 97.46 | -0.4108 | 74% | 16% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **33.4%** | **83.2%** | **84.5%** | **84.5%** | **84.5%** | **74.0%** |
| **Partly employed**  | **56.4%** | **6.6%** | **5.3%** | **5.3%** | **5.3%** | **15.8%** |
| Offered e, chose P  | 51.1% | 1.3% | 0.0% | 0.0% | 0.0% | 10.5% |
| Offered p, chose P  | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% |
| **Unemployed**  | **10.2%** | **10.2%** | **10.2%** | **10.2%** | **10.2%** | **10.2%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% |


---


### π=0.2, lower partial hours 12.0 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 0.5 | 600 | 15.11% | -0.0 | -0.4997 | 74% | 16% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **33.1%** | **83.2%** | **84.5%** | **84.5%** | **84.5%** | **73.9%** |
| **Partly employed**  | **56.7%** | **6.6%** | **5.3%** | **5.3%** | **5.3%** | **15.8%** |
| Offered e, chose P  | 51.4% | 1.3% | 0.0% | 0.0% | 0.0% | 10.5% |
| Offered p, chose P  | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% |
| **Unemployed**  | **10.2%** | **10.2%** | **10.2%** | **10.2%** | **10.2%** | **10.2%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% |


---


### π=0.3, lower partial hours 12.0 

Basic Version with no bonus:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 0.5 | 0 | 5.61% | 0.0 | -0.5561 | 84% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **84.5%** | **84.5%** | **84.5%** | **84.5%** | **84.5%** | **84.5%** |
| **Partly employed**  | **5.3%** | **5.3%** | **5.3%** | **5.3%** | **5.3%** | **5.3%** |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% |
| **Unemployed**  | **10.2%** | **10.2%** | **10.2%** | **10.2%** | **10.2%** | **10.2%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% |


---


### π=0.3, lower partial hours 12.0 

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 0.5 | 600 | 5.61% | 132.9 | -0.3732 | 62% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **1.8%** | **55.8%** | **84.5%** | **84.5%** | **84.5%** | **62.2%** |
| **Partly employed**  | **64.5%** | **33.9%** | **5.3%** | **5.3%** | **5.3%** | **22.9%** |
| Offered e, chose P  | 59.2% | 28.6% | 0.0% | 0.0% | 0.0% | 17.6% |
| Offered p, chose P  | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% |
| **Unemployed**  | **33.7%** | **10.3%** | **10.2%** | **10.2%** | **10.2%** | **14.9%** |
| Offered e, chose U  | 23.5% | 0.1% | 0.0% | 0.0% | 0.0% | 4.7% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% |


---


### π=0.3, lower partial hours 12.0 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 0.5 | 600 | 18.22% | -0.0 | -0.4901 | 62% | 23% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **1.7%** | **55.6%** | **84.5%** | **84.5%** | **84.5%** | **62.1%** |
| **Partly employed**  | **62.8%** | **34.0%** | **5.3%** | **5.3%** | **5.3%** | **22.5%** |
| Offered e, chose P  | 57.5% | 28.7% | 0.0% | 0.0% | 0.0% | 17.2% |
| Offered p, chose P  | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% | 5.3% |
| **Unemployed**  | **35.5%** | **10.5%** | **10.2%** | **10.2%** | **10.2%** | **15.3%** |
| Offered e, chose U  | 25.3% | 0.3% | 0.0% | 0.0% | 0.0% | 5.1% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% | 10.2% |

















---



layout: true
class: header

<h2 style="background-color: #fdd;">With Original Values for χ</h2>


---

This uses the value fo χ used in previous experiments:


$$\chi = 
\begin{bmatrix}
    \chi(e,e) & \chi(e,p) & \chi(e,u) \\
    \chi(p,e) & \chi(p,p) & \chi(p,u) \\
    \chi(u,e) & \chi(u,p) & \chi(u,u) 
\end{bmatrix} = 
\begin{bmatrix}
    0.94 & 0.03 & 0.03 \\
    0.57 & 0.33 & 0.1 \\
    0.4 & 0.1 & 0.5
\end{bmatrix}
$$

which yields stationary distribution (with perfect enforcement) of:

| E | P | U |
|:-:|:-:|:-:|
| 88.77% | 4.92% | 6.31% |




---

### π=0.2, lower partial hours: 12

Basic Version with no bonus:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 0.5 | 0 | 3.38% | 0.0 | -0.5323 | 89% | 5% |

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


### π=0.2, lower partial hours: 12

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 0.5 | 600 | 3.38% | 79.74 | -0.4262 | 80% | 14% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **43.3%** | **88.7%** | **88.8%** | **88.8%** | **88.8%** | **79.7%** |
| **Partly employed**  | **50.4%** | **5.0%** | **4.9%** | **4.9%** | **4.9%** | **14.0%** |
| Offered e, chose P  | 45.4% | 0.1% | 0.0% | 0.0% | 0.0% | 9.1% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.2, lower partial hours: 12

Now adjust the taxes to remove the deficit when the bonus is in place:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.2 | 0.5 | 600 | 10.53% | 0.0 | -0.491 | 80% | 14% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **43.2%** | **88.7%** | **88.8%** | **88.8%** | **88.8%** | **79.7%** |
| **Partly employed**  | **50.5%** | **5.0%** | **4.9%** | **4.9%** | **4.9%** | **14.0%** |
| Offered e, chose P  | 45.5% | 0.1% | 0.0% | 0.0% | 0.0% | 9.1% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.3, lower partial hours: 12

Basic Version with no bonus:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 0.5 | 0 | 3.38% | -0.0 | -0.5323 | 89% | 5% |

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


### π=0.3, lower partial hours: 12

Now add the 600 dollar bonus without changing tax rate:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 0.5 | 600 | 3.38% | 106.32 | -0.3858 | 67% | 24% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **1.9%** | **66.9%** | **88.8%** | **88.8%** | **88.8%** | **67.0%** |
| **Partly employed**  | **78.2%** | **26.8%** | **4.9%** | **4.9%** | **4.9%** | **23.9%** |
| Offered e, chose P  | 73.2% | 21.8% | 0.0% | 0.0% | 0.0% | 19.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **19.9%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **9.0%** |
| Offered e, chose U  | 13.6% | 0.0% | 0.0% | 0.0% | 0.0% | 2.7% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.3, lower partial hours: 12

Now adjust the taxes to remove the deficit when the bonus is in place:

| π0 | π1 | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.3 | 0.5 | 600 | 13.47% | 0.0 | -0.4762 | 67% | 24% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | **1.8%** | **67.3%** | **88.8%** | **88.8%** | **88.8%** | **67.1%** |
| **Partly employed**  | **78.7%** | **26.4%** | **4.9%** | **4.9%** | **4.9%** | **24.0%** |
| Offered e, chose P  | 73.7% | 21.5% | 0.0% | 0.0% | 0.0% | 19.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | **19.5%** | **6.3%** | **6.3%** | **6.3%** | **6.3%** | **8.9%** |
| Offered e, chose U  | 13.2% | 0.0% | 0.0% | 0.0% | 0.0% | 2.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
















---

layout: true

## Comparison of Results from two example χ:

Below, χ1 refers to the original χ (pink slides),
while χ2 refers to the modified χ (green slides).

---

Basic Version, no bonus:

| | E | P | U |
|:-:|:-:|:-:|:-:|
| χ1, π=0.2 | 88.8% | 4.9% | 6.3% |
| χ2, π=0.2 | 84.5% | 5.3% | 10.2% |
| χ1, π=0.3 | 88.8% | 4.9% | 6.3% |
| χ2, π=0.3 | 84.5% | 5.3% | 10.2% |

---

Now add the 600 dollar bonus without changing tax rate:

| | E | P | U |
|:-:|:-:|:-:|:-:|
| χ1, π=0.2 | 79.7% | 14.0% | 6.3% |
| χ2, π=0.2 | 74.0% | 15.8% | 10.2% |
| χ1, π=0.3 | 67.0% | 23.9% | 9.0% |
| χ2, π=0.3 | 62.2% | 22.9% | 14.9% |

---

Now adjust the taxes to remove the deficit when the bonus is in place:

| | E | P | U |
|:-:|:-:|:-:|:-:|
| χ1, π=0.2 | 79.7% | 14.0% | 6.3% |
| χ2, π=0.2 | 73.9% | 15.8% | 10.2% |
| χ1, π=0.3 | 67.1% | 24.0% | 8.9% |
| χ2, π=0.3 | 62.1% | 22.5% | 15.3% |

















---

layout: true

## Some Empirical Notes:

---

### Average Hours for Part-time workers

- Average hours for part-time workers in CPS data: 22-23 hours.
- But CPS defines part-time as no more than 35 hours per week.
- Conditional on working 1-20 hours, the average is 14-15.
- So lower value for $ĥ_p$ is reasonable.

<img src="img/2023aug23/Average hours worked last week for those who worked 1-20 hours (IPUMS CPS).png" style="width:100%;">


---

### Labor Market Composition Over Time

The following graph ignores those not at work or not in the labor force:

<img src="img/2023aug23/CPS IPUMS Labor Market Composition (ignoring not at work).png" style="width:100%;">

<!--![](img/2023aug23/CPS%20IPUMS%20Labor%20Market%20Composition.png)-->


---

### Does Part-Time employment have a spike like PUI?

- During the pandemic, both full and partial UI spiked upwards. Moreover, PUI increased as a *share* of total UI benefits.
- In CPS, part-time employment did spike upwards, but relatively less than unemployment did. This results in the opposite pattern in ratio of P to U as seen in UI.

<img src="img/2023aug23/CPS%20IPUMS%20P%20as%20share%20of%20P%20and%20U%20(rate).png" style="width:100%;">

---

### Does Part-Time employment have a spike like PUI?

- During the pandemic, both full and partial UI spiked upwards. Moreover, PUI increased as a *share* of total UI benefits.
- In CPS, part-time employment did spike upwards, but relatively less than unemployment did. This results in the opposite pattern in ratio of P to U as seen in UI.

<img src="img/2023aug23/CPS%20IPUMS%20P%20as%20share%20of%20P%20and%20U%20(sub20).png" style="width:100%;">

<span style="font-size:small;">(Above: Same graph but with part-time work restricted to those who work 20 hours or less.)</span>









