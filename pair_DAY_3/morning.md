## Morning (pair research — Day 3)

**Plan for today**

We held a short meeting and talked through the topics we wanted to cover for this pair block—LoRA, rank, and how fine-tuning might change a critic’s behavior when the input evidence is uncertain. After that alignment, I finished drafting the research question on LoRA, rank, and how adapters might push a critic toward confident versus cautious scoring when evidence is thin. I am handing that question to my peer so they can do their own reading and write the explainer answer from their angle.

**What I want from the exchange**

I hope their write-up connects the math of LoRA (the low-rank update on frozen weights) to behavior on ambiguous inputs, and that they either confirm or challenge the idea that higher rank on a tiny preference set can look like memorization rather than rubric learning. I will read their explainer with our shared training setup in mind (small ORPO run, wide confidence intervals) and note anything I should change before the next ablation.
