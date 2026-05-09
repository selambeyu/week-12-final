# Asker Sign-Off

**Status:** Closed

Before this explainer, I knew I should “bootstrap deltas” on the bench, but I could not **derive** why **unpaired** resampling is wrong for **same-task** comparisons or **quantify** how wrong in **width** and **decision** space.

I now understand the load-bearing points:

- **Paired data** means the **task index** is the unit; **independent** resampling of columns **destroys** \(\mathrm{Cov}(A,B)\) when methods co-move with difficulty.
- **Variance of the mean difference** is **not** the sum of separate column variances under pairing; dropping covariance **widens** CIs and **biases toward “no deploy.”**
- At **plausible** \(\Delta\) and correlation, **method choice** can flip whether zero is inside the interval—even when the **point estimate** is unchanged.

**What I will do differently:** keep **paired** resampling as the **documented default** in `Sales-Evaluation-Bench`, report **task-level differences** transparently, and treat any **unpaired** CI on shared tasks as a **methodology bug**, not a “conservative” choice.

**Explicit scope:** This explainer does not replace **Bayesian** hierarchical models or **multiple-comparison** correction across many method variants; it closes the **bootstrap pairing** gap for the portfolio’s current eval design.

This closes the gap named in `question.md` and matches the mechanism story in `explainer.md`.
