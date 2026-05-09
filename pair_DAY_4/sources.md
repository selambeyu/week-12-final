## Sources

1. Efron & Tibshirani (1993) *An Introduction to the Bootstrap*, §9.6 — paired vs. two-sample bootstrap; formal derivation of variance reduction under positive correlation.
2. Berg-Kirkpatrick, Burkett & Klein (2012) "An Empirical Investigation of Statistical Significance in NLP" (*EMNLP 2012*) — paired bootstrap in NLP evaluation; shows that for same-test-set comparisons, unpaired methods are consistently anti-conservative relative to paired.
3. **Tool used:** `scipy.stats.bootstrap` with `paired=True` vs `paired=False` on a synthetic n=52 benchmark to reproduce the CI width ratios above.