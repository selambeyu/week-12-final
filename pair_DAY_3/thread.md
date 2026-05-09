# Tweet thread (4–6 posts) — LoRA rank vs. cautious scoring

**1/** Week 11 critic: ORPO + LoRA on ~51 pairs. Delta A CI touches zero. I asked: what does **rank** actually control—not just parameter count, but **confidence vs. hedging** when the email signal is weak?

**2/** LoRA freezes \(W\) and trains a skinny bypass: \(W_{\mathrm{eff}} = W + BA\). **Rank = how many directions** the adapter can move. It is not “more rank = strictly better”; it is “more **expressivity** you must **identify** from data.”

**3/** Intrinsic-dimension story (in one line): fine-tuning often lives in a **low-dimensional** subspace of weight space. If your **data** is tiny and homogeneous, a **big** subspace is mostly **unidentified** → surface pattern fit.

**4/** Behavioral read: **low rank** → adapter is a **small nudge** → pretrained **cautious** language can survive on ambiguous inputs. **High rank + small n** → room to **memorize** “pass-shaped” examples → can read as **overconfident** without true rubric depth.

**5/** Engineering move: print trainable params (`peft`), try **r ∈ {4,8}** on the **same** pairs, keep evaluation **paired** on the same tasks. Rank is a **hypothesis**, not a default.

**6/** Full write-up + sources (Hu et al. LoRA; Aghajanyan et al. intrinsic dim; PEFT demo) live in the Day 3 blog draft—this thread is the compress.
