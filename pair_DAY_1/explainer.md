# explainer.md

## What actually happens inside an LLM call (and why your latency + cost feel unpredictable)

You said you can measure latency and cost in your Week 10/11 system (sales agent + judge bench), but not explain what actually drives them. This explainer builds a concrete inference-time model of what is happening under the hood.

---

## 1. Every LLM call has two phases: prefill and decode

Even though an API call looks like a single operation, internally it is split into:

### 🔹 Prefill (prompt processing phase)

The model processes the entire input prompt in one forward pass:
- system prompt
- task instructions
- agent context (sales email, brief, rubric, etc.)

**What happens internally:**
- Self-attention is computed across all prompt tokens
- Each token produces **key and value vectors per transformer layer**
- These are stored in the **KV cache**

👉 This phase is parallel over tokens but scales with prompt length.

---

### 🔹 Decode (generation phase)

After prefill, the model generates tokens sequentially:

- token₁ conditioned on full KV cache
- token₂ conditioned on token₁ + KV cache
- token₃ conditioned on token₁–₂ + KV cache

Each step reuses cached attention states instead of recomputing the prompt.

👉 This phase is inherently serial.

---

## 2. The key latency equation

A useful systems-level abstraction is:

Latency ≈ Prefill(prompt_tokens) + Decode(output_tokens)

Or more intuitively:

- TTFT (time-to-first-token) ≈ O(prompt_length)
- Total generation time ≈ O(output_length)

👉 This separation is the core reason performance feels “non-linear.”

---

## 3. Why prompt length increases latency (but output length behaves differently)

### Prompt length affects prefill

Because the model must:
- attend over *all input tokens*
- construct KV cache from scratch

So longer prompts ⇒ more expensive **one-time full attention pass**

---

### Output length affects decode

Once prefill is done:
- KV cache is reused
- prompt is NOT recomputed

So each new token only attends to cached memory:

> output cost grows linearly per token, but without reprocessing the prompt

---

## 4. Why the start of the prompt has disproportionate influence

Transformers do not process text sequentially; instead:

- every token attends to all previous tokens
- early tokens remain present in KV cache throughout generation

Two key effects:

### 🔹 Instruction anchoring
System prompts act as global constraints:
- “be concise”
- “output JSON”
- “do not hallucinate”

These are embedded into attention structure during prefill and persist through decode.

---

### 🔹 KV cache persistence
The KV cache stores:
> per-layer attention key/value tensors for every prompt token

This means:
- prompt is not re-read
- but is continuously attended to during generation

So early tokens become **global steering signals**

---

## 5. Why KV cache is the real bottleneck abstraction

During prefill:
- keys/values are computed for each token across all layers

During decode:
- the model computes attention only for the **new token**
- it reuses cached KV tensors instead of recomputing the prefix

More precisely:
> KV cache stores per-layer attention keys and values so attention does not recompute over the full prefix at every decoding step

This is what makes generation efficient—but also why prompt size still matters heavily.

---

## 6. Why longer prompts increase cost more than longer outputs (important intuition)

A subtle but critical asymmetry:

### Prompt cost
- recomputed every request
- scales with full prompt length
- cannot be amortized across tokens

### Output cost
- incremental per token
- KV cache is reused

So:

> repeating long system prompts is one of the most expensive design patterns in production LLM systems

---

## 7. The key failure insight (what most people miss)

This leads to a non-obvious production implication:

> Reducing prompt length often improves latency more than optimizing output length

Because:
- prefill dominates TTFT for large contexts
- repeated system prompts are paid every single call
- decode optimization only affects marginal token cost

This is why prompt compression, caching, and retrieval trimming are high-impact engineering levers.

---

## 8. What this explains in your Week 10/11 system

This model clarifies three things you observed:

### 1. “Long prompts are slow”
Because prefill scales linearly with input tokens.

### 2. “System prompts steer behavior”
Because they are embedded into KV cache attention structure during prefill.

### 3. “Costs feel unpredictable”
Because total latency is a sum of two different scaling regimes:
- prefill (input-dependent)
- decode (output-dependent)

---

## 9. Bottom line mental model

If you only remember one thing:

- **Prefill = read + compress full prompt into KV cache**
- **Decode = generate token-by-token using cached memory**
- **KV cache = stored attention state that avoids recomputing the prompt**
- **Latency = prefill cost + decode cost (two different scaling laws)**

---

## Sources

1. Vaswani et al. (2017) — *Attention Is All You Need*  
https://arxiv.org/abs/1706.03762  
Introduces self-attention, the mechanism that enables KV caching in transformer inference.

2. Kwon et al. (2023) — *vLLM: PagedAttention for Efficient LLM Serving*  
https://arxiv.org/abs/2309.06180  
Explains KV cache management and memory-efficient inference systems used in production LLM serving.

3. Hugging Face Documentation — Text Generation & KV Cache  
https://huggingface.co/docs/transformers/main/en/llm_tutorial  
Practical explanation of how cached key-value states are reused during autoregressive decoding.