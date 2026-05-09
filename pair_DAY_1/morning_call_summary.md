# Morning Call Summary

**Draft question (v1)** was too broad: essentially “how does LLM inference work?” It would have produced a textbook answer and would not have forced a tight link to how I actually ship software.

**Partner push:** Tie the ask to **artifacts I already claim in Week 10/11**—a **sales agent** plus a **judge-backed eval bench**—and to the gap behind my latency/cost talk: I can quote **duration and dollars** but not **what work the stack is doing** on each call. They asked me to name **one** thread I could pull: *prompt vs generated tokens*, *when a long fixed prefix matters*, *why the beginning of the prompt steers the whole completion*, and **which few numbers** I should log so I am not reverse-engineering behavior from a single end-to-end timer.

**Movement to final `question.md`:** We rewrote the ask so it is **diagnostic** (decompose the black box), **grounded** (Week 10 agent, Week 11 bench), and **Resolvable** in a short explainer—not a survey of all of serving. We dropped vague “explain transformers” language and locked the bullets my partner needs to answer in plain language.

**Plan for the rest of the day:** Each of us does **targeted reading** (serving docs, KV cache tutorials, one paper if needed), drafts our **evening question + explainer outline**, then meets **in the evening** to **trade questions and explain answers** so Day 1 ends with a closed loop, not more bookmarked tabs.
