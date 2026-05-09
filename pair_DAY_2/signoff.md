# Asker Sign-Off

**Status:** Closed

Before this explainer, I knew I wanted **valid JSON** and stable judge fields, but I was fuzzy on **what actually changes at the next-token step** when I rely on instructions alone versus when the stack enforces a **schema or grammar**. I tended to lump both under “prompt engineering” and was surprised when the model still **broke the contract** in edge cases.

I now understand the load-bearing distinction at the level I need for forward-deployed work:

- **Prompt-only control** reshapes **logits** so compliant tokens are more likely, but the model still draws from the **full vocabulary** unless something else intervenes—so preamble text, extra keys, bad enum strings, and minor syntax slips remain **possible** under sampling.
- **Schema- / grammar-constrained decoding** recomputes, after each prefix, which next tokens **keep the output valid**, **masks** illegal choices to zero probability, and **renormalizes** over what remains—the model still chooses, but only among **legal** continuations at that step.
- That is the mechanism behind **fewer parse failures and invalid tool arguments**: not “smarter JSON,” but **harder boundaries on the output language** at generation time.
- **Reliability of form is not reliability of judgment**: forcing `pass | fail | needs_review` does not make the verdict **correct** on ambiguous examples; it makes downstream code **integrable** without brittle cleanup.

**What I will do differently:** treat judge and tool outputs as **typed interfaces**—use constrained / structured outputs where the provider supports them, keep prompts for **semantics**, and keep **evals and spot checks** for **behavior**, not just **parse success**.

**Explicit scope:** This explainer does **not** replace reading my vendor’s exact **Structured Outputs / JSON mode** semantics, **partial JSON streaming**, or **refusal** behavior when no valid completion exists; those are implementation follow-ups once the prompt-vs-mask mental model is clear.


