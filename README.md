# econ3916-lab07-bootstrapping
# Estimation & Bootstrapping — Quantifying Uncertainty Without a Formula

## Objective
I measured how uncertain an estimate is, both with the textbook formula and with the bootstrap, and tested when each approach gives an honest answer.

## Methodology
- Loaded the UCI Adult Census Income data (32,561 respondents).
- Treated the full file as a population and drew repeated samples to separate the standard deviation of the data from the standard error of an estimate, checking the s/sqrt(n) relationship across four sample sizes.
- Built parametric confidence intervals from the Central Limit Theorem and plotted sampling distributions to see how fast the CLT takes hold for age and for capital gains.
- Ran the bootstrap by hand with a resampling loop, then with `scipy.stats.bootstrap`.
- Bootstrapped the median of age to see what happens when the data contain many ties.
- Compared percentile and BCa bootstrap intervals on a heavily skewed variable (positive capital gains).
- Bootstrapped a two-sample difference in mean weekly hours between men and women.
- Asked an AI to write a bootstrap-interval function, revised my prompt once, and checked the function against my own intervals.
- Ran a coverage simulation on lognormal data at n = 50 to check whether nominal 95% intervals actually cover 95% of the time.

## Key Findings
- The standard deviation describes how spread out people are and stays fixed. The standard error describes how precise the estimate is and shrinks with sqrt(n).
- The CLT converges quickly for age but slowly for capital gains, which are far more skewed, so the usual n > 30 rule of thumb is not enough for skewed data.
- The bootstrap standard error of the median of 32,561 whole-number ages is exactly 0.0000. Every resample returns the same median because so many ties pin it in place. The bootstrap is reporting a real property of the data, not failing.
- A bootstrap function written by AI needed an explicit seed before I could reproduce it and compare it with my own results.
- In the coverage simulation, for the mean, the nominal 95% parametric interval covered 92.5% and the percentile bootstrap covered 91.5%. That gap is inside the Monte Carlo standard error of about 1.3 points, so the two methods are indistinguishable here, and both under-cover slightly.
- For the median, the mean-centred parametric interval covered only about 66.8%, while the bootstrap held near its nominal level. When no formula exists for a statistic, borrowing the formula for a different one can be badly wrong, and the bootstrap avoids that.
