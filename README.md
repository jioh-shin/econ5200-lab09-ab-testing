# Diagnosing Experimental Failures in A/B Testing

## Objective
I examined common problems in A/B testing and how they affect the accuracy and reliability of experimental results.

## Methodology
- **CUPED:** Identified and fixed three bugs in variance reduction code and compared the results before and after the fixes.
- **Sample Ratio Mismatch (SRM):** Used chi-squared tests to check whether treatment and control groups had the expected sample sizes.
- **Marketplace Interference:** Simulated a marketplace with limited inventory to see how discounted buyers affect the control group and bias treatment effect estimates.
- **Bayesian A/B Testing:** Calculated the probability that B outperforms A and the expected loss of shipping B. I also ran a permutation test and wrote my own function to repeat the Bayesian analysis with more users.
- **Sequential Testing:** Simulated repeated significance testing across 1,000 experiments with no true effect to measure how peeking affects false positive rates.

## Key Findings
- After fixing the CUPED code, variance reduction increased from 0.0% to 82.7%, and the standard error decreased from 0.1539 to 0.0641.
- The SRM tests produced chi-squared statistics of 14.40 for a 0.60 percentage-point imbalance among 100,000 users and 20.00 for a 0.05 percentage-point imbalance among 20 million users. This showed me that even small imbalances can matter with large samples.
- In the marketplace simulation, the naive ATE was 0.1861, compared with 0.1428 when the discount was rolled out to everyone. The naive estimate overstated the effect by 23.3% of its value.
- In the Bayesian test, P(B > A) was 0.8866 and the expected loss of shipping B was 0.000473, so the shipping decision was False. The permutation test gave a p-value of 0.2302.
- When I applied my Bayesian function to a test with four times as many users, P(B > A) increased to 0.9951.
- With repeated peeking at 50 points, 32.4% of the 1,000 null experiments crossed p < 0.05 at least once, compared with 5.3% when testing only at the end.

Overall, I learned that coding errors, sample imbalances, interference between groups, and repeated testing can all lead to misleading A/B test results.
