# Asker Sign-Off

**Status:** Closed

Before this explainer, I knew LoRA added a **low-rank update** on top of frozen weights, but I treated **rank** mostly as a hyperparameter knob—not as a control on **how much of the pretrained “hedging” behavior** survives when evidence is thin, or why a **wide Delta A confidence interval** might co-occur with **high rank on a tiny preference set**.

I now understand the load-bearing mechanisms at the level I need for forward-deployed work:

- **Effective weights** follow \(W_{\mathrm{eff}} = W + BA\); only \(A\) and \(B\) train, and **rank bounds the dimensionality** of the adaptation, not its norm.
- **Low-rank updates** align with **intrinsic dimensionality**: many fine-tuning tasks need a small subspace of movement; **rank that exceeds what the data can identify** invites **memorizing surface patterns** instead of the rubric.
- On **ambiguous inputs**, a **smaller rank** often lets **pretrained calibration** show through; an **over-expressive adapter** on **dozens of pairs** can look **confident** for the wrong reasons.

**What I will do differently:** treat **rank vs. dataset size** as a **methodology claim** in the critic write-up, plan a **lower-rank ablation** on the same ORPO data, and report **paired** uncertainty for comparisons so we do not confuse **adapter expressivity** with **proven lift**.

**Explicit scope:** This explainer does not replace a full **learning-theory** treatment of generalization under preference optimization; it gives the **engineering** picture needed to defend rank choices in portfolio work.

This closes the gap named in `question.md` and matches the mechanism story in `explainer.md`.
