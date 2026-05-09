# Cohort Canon — Annotated Reading and Tool List for Forward-Deployed Engineers

This is a **curated, opinionated** list our cohort converged on during Week 12. Annotations focus on **when** to read each item and **what load-bearing mechanism** it clarifies—not on reproducing abstracts.

---

## Papers and primary technical reports

### Attention, transformers, and efficient serving

- **Vaswani et al., “Attention Is All You Need” (2017).**  
  **Read for:** what keys and values *are* in self-attention, and why autoregressive decoding can reuse them.  
  **FDE use:** explaining **prefill vs decode**, KV cache semantics, and why “long prompts” and “long outputs” stress different phases.

- **Kwon et al., “vLLM: PagedAttention for Efficient LLM Serving” (2023).**  
  **Read for:** how production systems **manage** KV cache memory under batching.  
  **FDE use:** moving from notebook latency to **serving economics**—fragmentation, paging, and why naive cache implementations thrash under load.

### Structured outputs and constrained decoding

- **Geng et al., “Grammar-Constrained Decoding for Structured NLP Tasks without Finetuning” (EMNLP 2023).**  
  **Read for:** the **mask illegal next tokens** viewpoint in a research framing.  
  **FDE use:** explaining why **grammar constraints** beat prompt-only JSON discipline for integration reliability.

- **Willard & Louf, “Efficient Guided Generation for Large Language Models” (2023).**  
  **Read for:** guided generation as a **decoding algorithm** problem, not a modeling problem.  
  **FDE use:** connecting vendor “structured output” features to **finite-state / grammar** intuitions.

### Adaptation and intrinsic dimensionality

- **Hu et al., “LoRA: Low-Rank Adaptation of Large Language Models” (2021).**  
  **Read for:** the **\(W + BA\)** update, rank ablations, and what rank *means* in capacity—not mysticism.  
  **FDE use:** defending adapter choices on **small** client datasets vs large internal corpora.

- **Aghajanyan et al., “Intrinsic Dimensionality Explains the Effectiveness of Language Model Fine-Tuning” (2020).**  
  **Read for:** why **low-dimensional** updates are expected even in huge models.  
  **FDE use:** pairing **rank** with **data scale** when a customer asks “why not train full fine-tune?”

### Evaluation statistics

- **Efron & Tibshirani, *An Introduction to the Bootstrap* (1993).**  
  **Read for:** paired vs two-sample resampling logic and **variance of differences**.  
  **FDE use:** benchmark A/B on **shared tasks**—the default in agent evals.

- **Berg-Kirkpatrick, Burkett & Klein, “An Empirical Investigation of Statistical Significance in NLP” (EMNLP 2012).**  
  **Read for:** why NLP papers historically mis-specified significance; paired structure matters.  
  **FDE use:** stopping **pseudo-rigorous** charts that confuse independent resampling with paired designs.

---

## Authoritative product and protocol documentation (not “secondary blogs”)

- **OpenAI: Structured Outputs / function calling guides.**  
  **Use when:** you need the **vendor-grounded** description of how schemas enter context and how tool calls are represented in API payloads.

- **Model Context Protocol (MCP) specification and overview.**  
  **Use when:** standardizing **tool servers** across engagements; pair with your own **schema + validation** discipline.

- **Your chosen provider’s rate-limit and concurrency documentation.**  
  **Use when:** writing **runbooks**; these numbers are **account-specific** but must be **first-class** design inputs.

---

## Engineering patterns worth memorizing

- **Prefill vs decode decomposition** for latency and cost narratives.  
- **Logit nudge vs token mask** for output reliability (prompting vs constrained decoding).  
- **Paired resampling of task IDs** for shared-eval comparisons.  
- **Exponential backoff with jitter** and **max retry bounds** for LLM client wrappers.  
- **Concurrency caps** distinct from RPM/TPM limits for tail latency control.  
- **Tool observability**: spans for **tool name, latency, status, argument size**—not only final assistant text.

---

## Tools our cohort actually ran

- **`scipy.stats.bootstrap`** — flip `paired=True` on shared-task score tables and **see** width change; builds gut feel fast.  
- **Hugging Face `transformers` LLM tutorial / KV cache docs** — tie API behavior to **cache tensors**.  
- **PEFT (`print_trainable_parameters`)** — makes adapter **capacity** legible before you defend a rank.  
- **`asyncio` semaphore + token bucket** — small harnesses that teach **tail latency** under burstiness.  
- **`pydantic` (or equivalent)** — validate tool arguments **before** side effects; cheap insurance in client work.

---

## How to use this list on an engagement

Start from the **failure mode** your customer fears (cost, latency, reliability, wrong decisions from evals), then pick **one primary source** and **one runnable check** from each relevant cluster. Week 12’s evidence-graph standard applies here too: if you cannot trace a claim to a **canonical** link or **runnable** demo, do not put it in front of a buyer’s engineering team.
