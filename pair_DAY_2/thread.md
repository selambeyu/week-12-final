# Twitter / LinkedIn thread (Day 2)

**Lead (optional):** Week 10 agent + Week 11 judge: I wanted to know how “say JSON only” differs from *actually* forcing JSON at decode time. Short thread: prompts vs schema-constrained generation.

---

**1/** The gap: prompt rules change what the model is *likely* to emit; a schema changes what it is *allowed* to emit—token by token. Same stack trace, very different reliability at the parser.

---

**2/** Prompt-only: each step still scores the full vocabulary. “Return only `{ verdict, reason, confidence }`” pushes `{`, quotes, enums—but “Here is the JSON:”, extra keys, `maybe` instead of an enum, or a trailing comma can still win a sample.

---

**3/** Schema / grammar decoding: after the prefix, a validator says which next tokens keep the output legal. Illegal tokens get probability 0; the rest renormalize. The model still chooses among *valid* continuations—it can’t step outside the grammar at that position.

---

**4/** Mental model: the prompt shifts preferences; the mask shrinks the **support** of the distribution. Soft nudge vs hard boundary. That’s why structured-output APIs cut format failures without replacing the need for good evals.

---

**5/** For a judge or tool-args contract, treat the JSON as an **interface**: enums, required fields, stable keys. Constrained decoding → fewer retries, less regex surgery, cleaner aggregation—assuming your provider/SDK exposes it.

---

**6/** Hard limit: schemas guarantee **form**, not **truth**. You can force `pass|fail|needs_review` and still be wrong on ambiguous cases. Use structure for integration reliability; use benchmarks + spot checks for behavioral reliability.


