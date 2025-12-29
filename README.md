Do Yelp Star Ratings Drive Revenue?

This project studies whether small changes in Yelp star ratings causally affect restaurant revenue, or whether higher revenue simply reflects higher underlying quality.

Yelp displays ratings in half-star increments, which creates a useful natural experiment: two restaurants with nearly identical true scores can end up in different visible rating buckets. I use this discontinuity to isolate the impact of the star badge itself.

Motivation

Star ratings play an outsized role in consumer decision-making, but it’s not obvious whether they cause better outcomes or merely summarize quality.

From a business perspective, this matters because:

Small rating changes are common

Reputation management is costly

If stars directly drive revenue, marginal improvements near thresholds may have outsized returns

The goal here is to separate signal (quality) from display (stars).

Data

Yelp restaurant-level data

Outcome: log revenue (logrev)

Running variable: true Yelp score (score)

Treatment: crossing a half-star rating threshold

Ratings are rounded mechanically, which allows comparison of restaurants just below vs. just above each cutoff.

Strategy
Regression Discontinuity Design (RDD)

I center each restaurant’s score around the nearest half-star cutoff and compare outcomes locally on either side.

Key idea:

If quality evolves smoothly, revenue should also evolve smoothly

Any sharp jump at the cutoff can be attributed to the star rating itself

I implement RDD in two ways:

Manual local linear regression with an interaction between distance-to-cutoff and treatment

rdrobust, which applies best-practice bandwidth selection, kernel weighting, and bias correction

Both approaches estimate the same causal quantity:
the discrete jump in revenue from gaining a half star.

Manipulation Check

A core RD assumption is that agents cannot precisely manipulate the running variable.

To test this, I examine the distribution of true scores:

Plot a histogram of scores

Overlay half-star cutoffs

Look for bunching just above thresholds

Result:
There is no visible spike or bunching around cutoffs, suggesting restaurants are not systematically manipulating scores to gain higher star ratings.

Results

There is a large and statistically significant jump in revenue at half-star thresholds

Manual RDD estimates suggest an increase of roughly 120–130%

Bias-corrected rdrobust estimates suggest effects closer to 180–200%

Confidence intervals are wider under rdrobust, but the effect remains highly significant

Importantly:

Revenue trends smoothly below the cutoff

The jump occurs exactly at the threshold

Results are stable across bandwidth choices and estimation methods

Interpretation

The findings indicate that:

Yelp star ratings are not just passive summaries of quality

The discrete star rating acts as a badge materially affecting consumer behavior

Visibility and platform design amplify small underlying differences into large economic outcomes

In short:

Gaining a half star can plausibly double restaurant revenue, even when true quality is held constant locally.

Why This Matters

For restaurant owners

Small improvements near rating thresholds may yield outsized returns

For platforms

Rating system design has real economic consequences

Monitoring manipulation and incentive effects is critical


Repository Structure

Notebook: full analysis, visualizations, and robustness checks

README: summary of motivation, method, and results