# Do Yelp Stars Influence Revenue?

**Question:**  
Do small changes in displayed Yelp star ratings *causally* affect restaurant revenue, or do higher revenues simply reflect higher underlying quality?

This project uses a **Regression Discontinuity Design (RDD)** to isolate the causal effect of crossing a half-star rating threshold on restaurant revenue.

## Why This Matters

- Yelp ratings are highly visible and updated frequently  
- If ratings causally drive revenue, reputation management has real ROI  
- If not, does higher revenue reflect better underlying quality?

Understanding this distinction matters for:
- restaurant owners
- platform designers

## Key Insight

Yelp displays ratings in **half-star increments**.

Two restaurants with nearly identical underlying scores can:
- appear in **different rating buckets**
- receive very different consumer attention

This creates a **natural experiment** at each half-star cutoff.

## Methodology: Regression Discontinuity Design (RDD)

We exploit the discontinuity at half-star thresholds:

- **Running variable:** centered Yelp score (distance from cutoff)
- **Treatment:** crossing the half-star threshold
- **Outcome:** log restaurant revenue

Key assumption:
> Restaurants just above and just below the cutoff are comparable in quality.

We estimate the treatment effect using two complementary approaches:

### 1. Manual RDD (Local Linear OLS)
- Local linear regression within a bandwidth around the cutoff
- Transparent and easy to interpret

### 2. `rdrobust`
- Data-driven bandwidth selection
- Robust inference optimized for RDD settings

## Manipulation Check

A key threat to RDD validity is **strategic manipulation** of the running variable.

We test this by examining the distribution of true Yelp scores around half-star cutoffs.

**Result:**
- No visible spikes or bunching around thresholds
- Suggests restaurants are *not* precisely manipulating ratings
- Supports the credibility of the RDD design

## Results Summary

- Based on p-values and Confidence Intervals, we see that crossing a half-star threshold leads to a **statistically significant increase in revenue**
- Manual OLS and `rdrobust` estimates are directionally consistent, although `rdrobust` produces wider confidence intervals due to bias correction
- Estimated revenue increases range from ~125% to ~195% locally at the half-star cutoff

**Interpretation:**  
Crossing a half-star rating threshold causes a discrete increase in revenue for restaurants near the cutoff (independent of underlying quality).

