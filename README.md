# A/B Test Analysis: CTR Improvement

## Overview
This project contains the analysis of an A/B test evaluating the impact of a new variant (Test) on user behavior compared to the current version (Control). The primary metric is **CTR (Click-Through Rate)**. The analysis was conducted using three approaches:

1. Aggregated metrics / A/B test calculator  
2. Bootstrap resampling  
3. Statistical tests (Parametric / Non-parametric)  

Additionally, users were segmented by the number of views (1–5, 6–10, 11+), and interaction effects were tested using ANOVA.

---

## Hypotheses

**Null Hypothesis (H0):**  
- There is no difference in CTR between the Control and Test variants.  

**Alternative Hypothesis (H1):**  
- The Test variant improves CTR compared to the Control variant.  

Segment-specific hypotheses:  

- **H0_segment:** CTR is the same between Test and Control for each user segment (1–5, 6–10, 11+ views).  
- **H1_segment:** CTR is higher for Test compared to Control in at least one segment.

---

## Project Files
| File | Description |
|------|-------------|
| `abtest_python.ipynb` | Jupyter Notebook containing the full analysis: EDA, bootstrap, hypothesis testing, segmentation |
| `data.csv` | Input A/B test dataset |
| `README.md` | Project description and results |

---

## Libraries Used
- pandas, numpy  
- matplotlib, seaborn  
- scipy.stats  
- statsmodels  

---

## Analysis Steps
1. **Exploratory Data Analysis (EDA)**
   - Checked for missing values and data types
   - Plotted histograms, violin plots, and CTR distributions
2. **Aggregated Metrics**
   - Calculated CTR (`clicks / views`)
   - Compared total clicks and views between groups
3. **Bootstrap**
   - Resampling to estimate mean CTR
   - Calculated uplift (%) and 95% confidence intervals
   - Estimated probability that Test > Control
4. **Statistical Tests**
   - Checked normality (Shapiro)
   - Tested homogeneity (Levene)
   - Applied T-test or Mann–Whitney U test based on assumptions
5. **User Segmentation**
   - Groups by number of views: 1–5, 6–10, 11+
   - Evaluated CI and uplift for each segment
6. **ANOVA**
   - Tested interaction effect between group and number of views

---

## Results

### Traffic by Segment
| Views | Control | Test | Δ (%) |
|-------|--------|------|-------|
| 1–5   | 29,230 | 28,982 | -0.85 |
| 6–10  | 6,934  | 7,050  | +1.67 |
| 11+   | 3,836  | 3,968  | +3.44 |
| **Total** | 40,000 | 40,000 | 0.00 |

### CTR by Segment
| Views | Control CTR | Test CTR | Uplift (%) |
|-------|------------|----------|------------|
| 1–5   | 6.91%      | 8.04%    | 16.39      |
| 6–10  | 6.90%      | 8.03%    | 16.32      |
| 11+   | 6.99%      | 8.00%    | 14.49      |
| **Total** | 6.92%      | 8.04%    | 16.19      |

### Bootstrap Confidence Intervals
| Views | 90% CI Uplift (%) |
|-------|------------------|
| 1–5   | 12.5 – 20.4      |
| 6–10  | 12.0 – 20.6      |
| 11+   | 10.7 – 18.6      |

### ANOVA
- **Group**: p ≈ 1.6e-21 ✅ significant factor  
- **Number_of_views**: p ≈ 0.99 ❌ not significant  
- **Interaction (group × views)**: p ≈ 0.96 ❌ not significant  

---

## Conclusion
- The Test variant significantly increases CTR (~16%) across all segments.  
- The effect is stable and statistically significant.  
- No interaction effect was observed → Test performs equally well for all user groups.
- **Overall hypothesis confirmed:** the Test variant outperforms the Control variant.  
- **Segment-specific hypotheses:** CTR improvement is significant in all segments, confirming the Test performs well regardless of user activity.   
- **Recommendation:** rollout Test to 100% of users.

---

## Recommendations for Next Steps
1. Roll out the Test variant to all users.  
2. Monitor downstream metrics: conversion, revenue, retention.  
3. Plan further A/B tests for CTA, visual changes, or personalization.  

---

## Author
Anastasiia Voitsitska
