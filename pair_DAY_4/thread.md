# Tweet thread — paired vs. unpaired bootstrap on the same eval set

**1/** Same 52 tasks, two methods, scores \((a_i,b_i)\). You want a CI on **mean(a−b)**. Unpaired bootstrap **breaks the pairs** → wrong model → often **much wider** intervals.

**2/** Paired bootstrap: resample **tasks** with replacement; keep \((a_i,b_i)\) glued. Preserves **within-task correlation** when both methods struggle on the same hard emails.

**3/** \(\mathrm{Var}(A-B)=\mathrm{Var}(A)+\mathrm{Var}(B)-2\mathrm{Cov}(A,B)\). Unpaired effectively drops **Cov** when it is **positive** → **inflates** variance → **anti-precise**.

**4/** Toy case: critic wins every task by **+0.03** with zero spread. Paired CI nails **+0.03**. Unpaired can **cross zero** on the **same** numbers—**deploy** vs **don’t** from **method error**.

**5/** With shared benchmarks, **ρ** is often high; width ratios blow up fast. For FDE: **paired** is the default; unpaired is for **different** test populations.

**6/** Blog + `scipy.stats.bootstrap(..., paired=True)` demo trace in repo sources—read before you A/B a **Conversion-Engine** change on a fixed bench.
