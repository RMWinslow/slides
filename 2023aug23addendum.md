---
title: "Office Hours: 2023 Aug 23 (Addenda)"
layout: presentation_solar
---
<style>
th,td {font-size: smaller;}
</style>


<!--
## Outline:

- Tables for different enforcement rates. π=0.1,0.2,0.3, etc.
  - Table format updated to include more details.
  - Tables with same thing but with π0 or πu set to 0.
- Graph show how the employment of the 5 quintiles varies with different levels of π.
- Interpolation between two tax levels in π=0.5 case.
- Manual check that in the π=0.5 case, the additional taxes are exactly enough to pay for the additional benefits.

layout: true
class: header

<h2 style="background-color: #9cd6e4;">Further Experiments with π</h2>
-->


### π=0.0 

Basic Version with no bonus:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.0 | 0.5 | 0 | 3.34% | -0.0 | -0.5246 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% |
| **Partly employed**  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.0 

Now add the 600 dollar bonus without changing tax rate:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.0 | 0.5 | 600 | 3.34% | 62.02 | -0.4291 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% |
| **Partly employed**  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.0 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.0 | 0.5 | 600 | 9.28% | 0.0 | -0.4825 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% |
| **Partly employed**  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.1 

Basic Version with no bonus:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.1 | 0.5 | 0 | 3.34% | 0.0 | -0.5246 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% |
| **Partly employed**  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.1 

Now add the 600 dollar bonus without changing tax rate:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.1 | 0.5 | 600 | 3.34% | 70.88 | -0.4265 | 81% | 12% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 51.3% | 88.7% | 88.8% | 88.8% | 88.8% | 81.2% |
| **Partly employed**  | 42.4% | 5.0% | 4.9% | 4.9% | 4.9% | 12.4% |
| Offered e, chose P  | 37.5% | 0.1% | 0.0% | 0.0% | 0.0% | 7.5% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.1 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.1 | 0.5 | 600 | 9.78% | 0.0 | -0.4845 | 81% | 13% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 50.9% | 88.6% | 88.8% | 88.8% | 88.8% | 81.2% |
| **Partly employed**  | 42.8% | 5.0% | 4.9% | 4.9% | 4.9% | 12.5% |
| Offered e, chose P  | 37.9% | 0.1% | 0.0% | 0.0% | 0.0% | 7.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.2 

Basic Version with no bonus:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.5 | 0 | 3.34% | 0.0 | -0.5246 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% |
| **Partly employed**  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.2 

Now add the 600 dollar bonus without changing tax rate:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.5 | 600 | 3.34% | 97.46 | -0.3875 | 60% | 34% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 1.8% | 32.8% | 88.6% | 88.8% | 88.8% | 60.2% |
| **Partly employed**  | 91.9% | 60.8% | 5.1% | 4.9% | 4.9% | 33.5% |
| Offered e, chose P  | 86.9% | 55.9% | 0.2% | 0.0% | 0.0% | 28.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.2 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.2 | 0.5 | 600 | 12.78% | 0.0 | -0.4718 | 60% | 34% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 1.2% | 33.0% | 88.6% | 88.8% | 88.8% | 60.1% |
| **Partly employed**  | 92.5% | 60.7% | 5.1% | 4.9% | 4.9% | 33.6% |
| Offered e, chose P  | 87.6% | 55.8% | 0.2% | 0.0% | 0.0% | 28.7% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.3 

Basic Version with no bonus:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.5 | 0 | 3.34% | 0.0 | -0.5246 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% |
| **Partly employed**  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.3 

Now add the 600 dollar bonus without changing tax rate:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.5 | 600 | 3.34% | 150.62 | -0.3343 | 44% | 50% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 0.0% | 1.2% | 39.8% | 88.8% | 88.8% | 43.7% |
| **Partly employed**  | 93.7% | 92.5% | 53.9% | 4.9% | 4.9% | 50.0% |
| Offered e, chose P  | 88.8% | 87.6% | 49.0% | 0.0% | 0.0% | 45.1% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.3 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.3 | 0.5 | 600 | 17.46% | -0.0 | -0.4587 | 44% | 50% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 0.0% | 1.1% | 39.2% | 88.8% | 88.8% | 43.6% |
| **Partly employed**  | 93.7% | 92.5% | 54.5% | 4.9% | 4.9% | 50.1% |
| Offered e, chose P  | 88.8% | 87.6% | 49.5% | 0.0% | 0.0% | 45.2% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.4 

Basic Version with no bonus:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.4 | 0.5 | 0 | 3.34% | 0.0 | -0.5246 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% |
| **Partly employed**  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.4 

Now add the 600 dollar bonus without changing tax rate:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.4 | 0.5 | 600 | 3.34% | 203.78 | -0.2808 | 34% | 55% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 0.0% | 0.0% | 2.7% | 78.1% | 88.8% | 33.9% |
| **Partly employed**  | 67.2% | 93.7% | 91.0% | 15.6% | 4.9% | 54.5% |
| Offered e, chose P  | 62.3% | 88.8% | 86.1% | 10.7% | 0.0% | 49.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 32.8% | 6.3% | 6.3% | 6.3% | 6.3% | 11.6% |
| Offered e, chose U  | 26.5% | 0.0% | 0.0% | 0.0% | 0.0% | 5.3% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.4 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.4 | 0.5 | 600 | 22.65% | -0.0 | -0.4511 | 34% | 54% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 0.0% | 0.0% | 2.6% | 78.5% | 88.8% | 34.0% |
| **Partly employed**  | 67.6% | 93.7% | 91.0% | 15.1% | 4.9% | 54.5% |
| Offered e, chose P  | 62.7% | 88.8% | 86.1% | 10.2% | 0.0% | 49.6% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 32.4% | 6.3% | 6.3% | 6.3% | 6.3% | 11.5% |
| Offered e, chose U  | 26.1% | 0.0% | 0.0% | 0.0% | 0.0% | 5.2% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.5 

Basic Version with no bonus:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 0 | 3.34% | -0.0 | -0.5246 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% |
| **Partly employed**  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.5 

Now add the 600 dollar bonus without changing tax rate:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 600 | 3.34% | 301.24 | -0.2231 | 20% | 53% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 0.0% | 0.0% | 0.0% | 9.9% | 88.8% | 19.7% |
| **Partly employed**  | 15.3% | 66.8% | 93.7% | 83.8% | 4.9% | 52.9% |
| Offered e, chose P  | 10.4% | 61.9% | 88.8% | 78.9% | 0.0% | 48.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 84.7% | 33.2% | 6.3% | 6.3% | 6.3% | 27.4% |
| Offered e, chose U  | 78.3% | 26.9% | 0.0% | 0.0% | 0.0% | 21.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |


---


### π=0.5 

Now adjust the taxes to remove the deficit when the bonus is in place:

| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 0.5 | 0.5 | 600 | 32.86% | -0.0 | -0.4999 | 19% | 53% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 | all |
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
| Weekly Income  | 372 | 592 | 886 | 1280 | 2323 |  |
| **Fully employed**  | 0.0% | 0.0% | 0.0% | 8.1% | 88.8% | 19.4% |
| **Partly employed**  | 14.6% | 64.6% | 93.7% | 85.6% | 4.9% | 52.7% |
| Offered e, chose P  | 9.7% | 59.7% | 88.8% | 80.6% | 0.0% | 47.8% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 85.4% | 35.4% | 6.3% | 6.3% | 6.3% | 27.9% |
| Offered e, chose U  | 79.1% | 29.1% | 0.0% | 0.0% | 0.0% | 21.6% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |




