# Grounding Commit Pointer

## Target edits to Week 10/11 artifacts

1. **`Sales-Evaluation-Bench/judge/` (or equivalent judge client)**  
   Prefer **structured / constrained outputs** (vendor JSON schema, grammar-constrained decoding, or equivalent) for verdict objects instead of **prompt-only** “return JSON” instructions.

2. **`Conversion-Engine/` agent tool and judge integration code**  
   Separate **semantic** instructions (rubric, ICP, style) from **format** guarantees: prompts carry meaning; the stack enforces parseable types (`pass | fail | needs_review`, required keys).

3. **`Sales-Evaluation-Bench/methodology_rationale.md` (or README)**  
   Add one paragraph stating the **logit nudge vs. token mask** distinction so reviewers see why occasional parse failures under sampling are expected without constrained decoding.

## Why this change matters

Week 10/11 systems fail in production on **integration**, not only on “model intelligence.” Grounding judge and tool outputs in **hard output constraints** matches the mechanism explained in the Day 2 explainer and reduces brittle cleanup paths in the evaluation bench and agent.
