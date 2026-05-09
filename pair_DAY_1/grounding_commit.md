# Grounding Commit Pointer

## Target edits to Week 10/11 artifacts

1. `Conversion-Engine/memo.md`
   - Replace the current "8-15 seconds" statement with a latency decomposition paragraph: queue/network/prefill/decode/postprocess.

2. `Conversion-Engine/README.md`
   - Add an "Inference Cost & Latency Decomposition" subsection with measurable fields and explicit caveats on cache hit rate.

3. `Sales-Evaluation-Bench/README.md` and `Sales-Evaluation-Bench/executive_memo.md`
   - Revise "85ms overhead" claim to specify measurement context (critic-stage decode delta at fixed prompt length), and add note that total call latency depends on prefill+decode mix.

## Why this change matters

These edits convert unsupported performance shorthand into mechanism-linked, auditable claims. That improves technical credibility for both portfolio projects and aligns with Week 12 evidence-graph standards.
