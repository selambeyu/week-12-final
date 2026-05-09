# Portfolio Update (Weeks 10–12) — For an FDE Hiring Manager

## What shipped before this week

In **Week 10** I shipped a **`Conversion-Engine`** sales agent that integrates LLM calls into a realistic outreach workflow. In **Week 11** I shipped **`Sales-Evaluation-Bench`**: a structured evaluation harness and critic-focused experimentation (including **preference optimization** and reporting intended for stakeholder decisions). Together, these artifacts demonstrate **ownership** of an end-to-end loop: instrumented system, benchmark, and iteration.

## What Week 12 changed

Week 12 did not replace those projects; it **strengthened the defensibility** of their claims. Across **four** grounding commits—documented day-by-day in `pair_DAY_1` … `pair_DAY_4`—I edited the portfolio so that performance, reliability, and statistical statements trace to **mechanisms** and **reproducible procedures**, not shorthand.

## The four improvements, collectively

1. **Inference literacy (prefill vs decode, KV cache intuition).**  
   Portfolio documentation now explains **what dominates latency** in agent and judge calls and which **metrics** must be logged to separate prompt growth from completion growth. This matters for client conversations about **cost** and **SLAs** where “it felt slow” must become **phase-aware** debugging.

2. **Structured outputs as an integration contract.**  
   Where the bench and agent depend on **machine-parseable** objects, the narrative now distinguishes **prompting** from **decoder-level constraints**—the difference between “usually JSON” and **integrable** outputs under sampling.

3. **Adapter methodology that matches data scale.**  
   The critic story now ties **LoRA rank** to **expressivity** and **dataset size**, aligning optimization choices (e.g., ORPO) with **capacity** claims. This is the kind of rigor that prevents fine-tuning work from collapsing into “we trained something.”

4. **Correct uncertainty for paired benchmarks.**  
   Evaluation reporting is anchored in **paired** resampling on **shared tasks**, with explicit reasoning about why **unpaired** bootstraps mis-state variance when methods co-move with difficulty. This protects **product decisions** from methodology artifacts that systematically favor **inaction**.

## Why this should matter in hiring

Forward-deployed engineers are hired to make systems **work** in customer environments: measurable, maintainable, and explainable under scrutiny. Weeks 10–11 showed I could **build**; Week 12 shows I can **audit** what I built, **teach** it, and **revise** artifacts when a mechanism was previously glossed over. That combination—**ship + defend + edit**—is the portfolio shape this program targets for FDE-grade evidence.

## Evidence location

Detailed questions, partner-reviewed explainers, call summaries, sign-offs, sources, and grounding pointers live in **`pair_DAY_1`–`pair_DAY_4`**. The cohort-facing canon is in **`canonical_list.md`**, and the week narrative in **`synthesis.md`**. Public blog and thread URLs should be listed in the repository **README** alongside this repo state.
