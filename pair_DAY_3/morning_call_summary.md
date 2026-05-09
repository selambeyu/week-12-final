## Morning Call Summary — Day 3

Topic: **Training and post-training mechanics — LoRA.**

The draft question named LoRA and rank but initially mixed in **optimizer narrative** (ORPO) without isolating what rank does to **weight-space expressivity**. The morning call separated those concerns: **rank is about the adapter subspace**, not the preference-loss shape.

The connection to portfolio work was sharpened by pinning **file-level anchors** (`train_lora_judge.py`, `ablation_results.json`, ~51 pairs) so the explainer could cite **concrete** capacity–data tension instead of generic fine-tuning advice.

Both partners agreed the resolvable scope for one post is **rank ↔ cautious vs. confident behavior on ambiguous inputs**, with **intrinsic dimensionality** as the adjacent concept—not a full treatment of all PEFT variants.

By the end of the call, the asker’s question was unambiguous: **how rank shapes output style under uncertainty** when evidence is thin, grounded in the **Week 11 critic** setup.
