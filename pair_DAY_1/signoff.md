# Asker Sign-Off

**Status:** Closed

Before this explainer, I treated each LLM call as a **single latency number** and could not explain **how much of the work was “reading the prompt” vs “emitting new tokens,”** or why **long contexts** and **long completions** show up differently in time and billing.

I now understand the load-bearing mechanism at the level I need for forward-deployed work:

- **Prefill** processes the **entire** prompt in one forward pass, builds **per-layer key/value tensors** into a **KV cache**, and largely drives **time-to-first-token (TTFT)**.
- **Decode** generates **one token at a time**, reusing the cache so the model does **not** re-run full attention over the whole prompt on every step.
- **Latency and cost** track **two scaling regimes**: roughly **Prefill(prompt length) + Decode(output length)**—which is why a single wall-clock figure felt opaque.
- **Early prompt tokens** (system instructions, rubric, style rules) stay in the KV cache for all decode steps, so they act as **global steering**, not disposable header text.
- **Prompt-heavy** designs pay **every request** on prefill; **output length** adds **serial** decode cost—so trimming or compressing **inputs** is often a higher leverage move than only shortening completions.

**What I will actually log** (minimum): **input tokens**, **output tokens**, and—when the provider or stack exposes it—**TTFT** and/or **prefill vs total generation** so I can tie **prompt vs generated text** to **time and price** instead of guessing.

**Explicit scope:** This explainer does **not** walk provider-specific **prefix cache** policies, **batching**, **quantization**, or **speculative decoding**; those are the next layer once this decomposition is second nature.

This closes the gap named in `question.md` and matches the mechanism story in `explainer.md`.
