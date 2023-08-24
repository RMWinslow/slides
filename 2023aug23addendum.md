---
title: "Office Hours: 2023 Aug 23 (Addenda)"
layout: presentation_solar
---

## Outline:

- Tables for different enforcement rates. π=0.1,0.2,0.3, etc.
  - Table format updated to include more details.
  - Tables with same thing but with π0 or πu set to 0.
- Graph show how the employment of the 5 quintiles varies with different levels of π.
- Interpolation between two tax levels in π=0.5 case.
- Manual check that in the π=0.5 case, the additional taxes are exactly enough to pay for the additional benefits.





---

layout: true
class: header

<h2 style="background-color: #9cd6e4;">Further Experiments with π</h2>

---


| π | $\theta$ | bonus | $\tau$ | deficit | mean $U$ | Fully Empl | Partly Empl |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
c:\Users\RMW\Documents\GitHub\papersdrafts\covid_unemployment\mymodel\PUI_Model.py:453: RuntimeWarning: invalid value encountered in multiply
  agg_util = np.nansum([λ[x]*U(c[x].clip(0),l[x]) for x in self.state_set])
| 0.5 | 0.5 | 0 | 3.34% | -0.0 | -0.5246 | 89% | 5% |

Employment rate by income quintile:

| Quintile | 1 | 2 | 3 | 4 | 5 |
|:--|:-:|:-:|:-:|:-:|:-:|
| **Fully employed**  | 88.8% | 88.8% | 88.8% | 88.8% | 88.8% |
| **Partly employed**  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| Offered e, chose P  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose P  | 4.9% | 4.9% | 4.9% | 4.9% | 4.9% |
| **Unemployed**  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |
| Offered e, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered p, chose U  | 0.0% | 0.0% | 0.0% | 0.0% | 0.0% |
| Offered u, chose U  | 6.3% | 6.3% | 6.3% | 6.3% | 6.3% |

