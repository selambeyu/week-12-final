
# evening_call_summary.md 

# Evening Call Summary


In the evening call, we reviewed both explainer submissions (DPO vs SFT and inference-time mechanics) and evaluated whether each explainer successfully closed its respective gap.

The goal of the discussion was not just to validate correctness, but to check whether each explanation was precise enough to connect mechanisms to real FDE systems (training pipelines and inference pipelines).

---

## Feedback on the DPO explainer (given by inference-time partner)

The inference-time explainer author noted that the DPO writeup was technically correct but initially over-attributed “performance improvement” to DPO in a way that blurred the distinction between:

- preference optimization (relative ranking of outputs)
- absolute task correctness (benchmark performance)

They highlighted that the key missing clarification was that DPO does not introduce new capabilities into the model; it only reshapes probability mass over outputs already reachable by the base model under a KL-constrained objective.

After discussion, the DPO explainer was revised to explicitly include:
- evaluation vs training objective mismatch as the main failure mode
- clarification that DPO optimizes log-probability gaps, not correctness directly
- clearer conditions under which DPO can and cannot improve benchmark performance

---

## Feedback on the inference-time explainer (given by DPO partner)

The DPO explainer author reviewed the inference-time mechanics writeup and found the explanation of prefill, decode, and KV cache to be strong and intuitive.

The main feedback was around tightening the KV cache definition and making the systems-level cost model more explicit.

Specifically, they suggested:
- clarifying that KV cache stores **per-layer key/value tensors from self-attention**, enabling reuse across decoding steps without recomputing full attention over the prompt
- making the latency decomposition more explicit as a sum of prefill and decode costs
- reinforcing the asymmetry between prompt cost (recomputed per request) and generation cost (incremental per token)

The inference-time explainer was updated to reflect these points and include a clearer latency equation.

---

## Joint outcome of the discussion

Both explainers were revised after peer feedback, and both authors converged on a shared systems-level insight:

- Inference-time systems are governed by a **two-phase computation model (prefill vs decode)** with different scaling laws
- Alignment training methods like DPO operate on **relative preference structure, not absolute correctness**
- In both cases, the key failure mode comes from **misalignment between optimization signal and evaluation signal**

The evening review helped refine both explanations from conceptual understanding into more precise, mechanism-level descriptions suitable for production FDE reasoning.