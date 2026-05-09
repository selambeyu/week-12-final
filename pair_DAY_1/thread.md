# Twitter thread 

**Lead (optional):** Sales agent (Week-10) + judge bench (Week-11): I knew latency & rough cost, but not what the model *does* per call. Quick thread on prefill vs decode + what to log.

---

**1/** I couldn’t defend how much was “prompt” vs “generated text,” when a long fixed system prompt helps, why the *start* of the prompt steers the whole reply, or which numbers to log so I stop guessing.

---

**2/** One API call = two phases. Prefill: forward pass over the *whole* prompt → builds KV cache; drives time-to-first-token. Not optional—it’s how the model “reads” your system + brief + rubric.

---

**3/** Decode: generate one token at a time, reusing KV cache—no full prompt recompute each step. Latency ≈ Prefill(prompt) + Decode(output). Two scaling laws, one dashboard number.

---

**4/** Prompt length → mostly prefill (every request pays it). Output length → decode (serial, but prompt stays cached). Long repeated system prompts = expensive habit. Trimming prompts often beats only shortening completions.

---

**5/** Start of the prompt matters: early tokens sit in KV cache for every decode step. “Be concise / JSON only / judge rules” = global steering—not text you “scroll past” after token one.

---

**6/** Maps to what I felt: big context feels slow (prefill); rubric steers hard (cache); bills feel random when I mix input-cost and output-cost in my head without splitting them.

---

**7/** Minimum logs: input tokens, output tokens, + if possible TTFT (or prefill ms) vs total gen. Tie time *and* money to which phase grew—not vibes.

---

**Closer (optional):** If you ship agents + evals: split prefill vs decode in your head (and metrics) before you optimize. Everything else gets easier.
