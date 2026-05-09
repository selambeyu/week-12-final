# Grounding Commit Pointer

## Target edits to Week 10/11 artifacts

1. **`Sales-Evaluation-Bench/` scripts (e.g. `compute_deltas.py`) and README**  
   State explicitly that **bootstrap units are task IDs** applied **jointly** to both methods; forbid independent column resampling for **shared-task** comparisons.

2. **`executive_memo.md` / CFO-facing summary**  
   When presenting **uncertainty on \(\Delta A\)**, include one sentence on **why pairing matters** (same leads, shared difficulty) so stakeholders do not misread a **wide unpaired** interval as “fundamental noise.”

3. **`ablation_results.json` commentary**  
   For the **Δ = +0.0025** result, note **robustness to CI flavor** (null under both paired and unpaired) while warning that **future** larger effects could be **hidden** by the wrong bootstrap.

## Why this change matters

Forward-deployed engineers live or die on **whether a measured lift is real enough to ship**. Grounding the bench in **correct paired uncertainty** prevents **systematic** under-deployment and makes the Week 11 evidence graph **auditable** under review.
