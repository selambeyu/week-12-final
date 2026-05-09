# Grounding Commit Pointer

## Target edits to Week 10/11 artifacts

1. **`training/train_lora_judge.py` (or config)**  
   Add a **rank sweep** or default **lower rank** (e.g. `r=8` or `r=4`) documented against **dataset size** (51 preference pairs). Keep a reproducible one-line rationale in comments.

2. **`Sales-Evaluation-Bench/methodology_rationale.md`**  
   Insert a short subsection **“LoRA rank vs. data scale”** linking **expressivity**, **intrinsic dimension**, and why **CI width** should be read together with **adapter capacity**, not only with optimizer choice (ORPO vs DPO).

3. **`ablations/ablation_results.json` narrative** (README or memo)  
   When Delta A intervals touch zero, frame the result as **under-identified at this margin** (small Δ, finite n) and list the **next ablation** (lower rank, more diverse pairs) instead of over-claiming a null.

## Why this change matters

The portfolio previously justified **post-training objective** without defending **adapter capacity**. Closing the LoRA gap turns the critic from a **black-box fine-tune** into a **testable hypothesis** about rank, calibration, and evidence strength—what a hiring manager can probe in a technical interview.
