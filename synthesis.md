# Week 12 Synthesis — Knowledge Gap Formulation for Compounding

This week traded shipping new surface area for **mechanism literacy** on the systems I already placed in a Weeks 10–11 portfolio: a **`Conversion-Engine` sales agent** and a **`Sales-Evaluation-Bench` with a trainable critic**. The paired loop forced a discipline I had avoided while moving fast: naming **one diagnostic gap per day**, defending it against a hostile reading of my own artifacts, and paying the learning back through **grounding commits** rather than abstract notes.

## The eight gaps closed (Days 1–4)

### Four I named (my questions)

1. **Inference-time accounting.** I could quote latency and rough cost, but not decompose an LLM call into **prefill vs decode**, nor explain why **prompt-heavy** designs and **long completions** show up differently in dashboards and bills. Closing this gap changed how I read Week 10 traces and Week 11 judge calls: **TTFT** is not “mystery latency,” it is largely **prompt processing and KV cache construction**; **serial decode** is where output length bites.

2. **Soft prompts vs hard output constraints.** I conflated “ask for JSON” with **guaranteeing JSON**. I needed a token-level story for why **schema- and grammar-constrained decoding** removes entire failure classes that **prompt-only** control leaves probable under sampling.

3. **LoRA rank as behavioral capacity, not a dial.** I treated rank as “more parameters must help,” without connecting **adapter expressivity** to **dataset size** and to **hedging vs overconfidence** on ambiguous inputs in a tiny ORPO run.

4. **Paired vs unpaired bootstrap on shared benchmarks.** I understood “bootstrap the delta” procedurally but not why **independent resampling of two score columns** drops the **covariance** induced by **shared tasks**, **widening** intervals and **biasing** deploy decisions toward “do nothing.”

### Four I researched and explained (authored explainers for partners)

5. **KV cache / paging and production inference.** For a partner working on long-context outreach summarization, I wrote a bridge from **Attention Is All You Need**’s use of keys and values to **PagedAttention**-style memory management—enough to explain **why serving systems** care about **cache fragmentation** and **batching**, not only FLOPs.

6. **Intervention tests for “reasoning” in LLM judges.** A partner’s judge emitted chain-of-thought before a verdict; I framed **corrupt/remove/reorder** interventions and **ablation of steps** to test whether trace text is **load-bearing** or **post-hoc narration**—the difference between **debuggable** evaluation and **theater**.

7. **DPO vs SimPO vs ORPO at the gradient narrative level.** Another partner needed a **one-post** intuition for what each objective **penalizes** when preferences disagree with the reference model; I centered **implicit constraints** (β, KL-ish terms, reference anchoring) and where **overoptimization** shows up in **production-ish** judges.

8. **LLM-as-judge biases in single-output scoring.** For a bench that scores **one** completion at a time, I separated **sampling variance** from **judge measurement bias** and gave **cheap** checks: **length correlation**, **rubric anchoring**, and **template sensitivity**—mitigations that do not require a second gold judge on day one.

## The most surprising thing I learned

The surprise was not a single paper fact but a **role reversal** in how I evaluate my own work. Under time pressure, I had been **over-identifying** with **architectural novelty** (“agent,” “judge,” “ORPO”) and **under-identifying** with **measurement mechanics** that dominate real deployments: **prefill/decode**, **masking**, **paired resampling**. Those sound like “details,” yet they are exactly where senior engineers press in reviews—and where mistakes **look like conservative science** (wide intervals, null results) when they are actually **method error** or **capacity illusions**.

## Canonical reading list and tool list I contributed to the cohort

I consolidated duplicates across days into a **cohort-facing canon** (see `canonical_list.md`). The highest-signal items I repeatedly pushed teammates toward were: **Vaswani et al.** and **vLLM/PagedAttention** for serving realism; **OpenAI structured outputs** plus **Willard & Louf** / **Geng et al.** for constrained decoding; **Hu et al.** and **Aghajanyan et al.** for adapter intuition; **Efron & Tibshirani** and **Berg-Kirkpatrick et al.** for **paired** resampling in NLP evaluation; and provider **function-calling** documentation where tool JSON meets models.

On tools, the cohort got the most mileage from **`scipy.stats.bootstrap(..., paired=True)`** as a **sanity check**, **`peft`**’s `print_trainable_parameters()` as a **capacity thermometer**, and **`pydantic`**-style validation sketches for **tool argument** safety where structured outputs meet backends.

## Trajectory and quality bar

If there is a trajectory worth grading, it is **diagnosticity**: questions moved from “what is X?” to “what decision does misunderstanding X break, on **this** artifact, with **these** numbers?” The public bar I held myself to was the program checklist: **two canonical citations** with links, a **runnable or inspectable** demonstration, **partner sign-off**, and **grounding commits** that a reviewer could diff against Weeks 10–11.

## What changed in how I read my own portfolio

Before this week, my Weeks 10–11 READMEs mixed **outcomes** (“judge improves conversion quality”) with **mechanism claims** that were sometimes **shorthand** (“fast enough,” “valid JSON,” “statistically sound”). The paired loop made that shorthand **expensive**: a partner could not write a good explainer without a **pinned artifact** and a **testable** statement, and I could not sign off without naming what I understood **after** revision that I did not understand before.

The practical effect is a portfolio that still tells a **customer story**, but now carries **engineer-trust** signals: where latency comes from, why structured outputs are not “just prompting,” why rank is reported next to dataset scale, and why bootstrap code resamples **tasks** jointly. Those signals matter for forward deployment because the buyer’s technical stakeholders rarely dispute that an LLM “can” do something; they dispute whether your system **keeps doing it** under **regressions** and **measurement** scrutiny.

## Cohort dynamics that compounded the learning

The cohort vote on topics did more than set a schedule; it created **shared vocabulary** across pairs. When Day 2’s winning topic was **structured generation**, multiple pairs produced **compatible** explainers from different angles—grammar constraints, API “structured outputs,” and tool-argument reliability. That redundancy was useful: it forced **cross-checking** primary sources instead of trusting a single blog post that elides masking details.

The morning and evening calls were load-bearing in the way the syllabus claims. Asynchronous text let us **polish sentences**; voice let us **expose hidden assumptions** (“when you say correlation, do you mean across tasks or across runs?”). The sharpest improvements in my questions came when my partner refused a **comfortable** abstraction and made me name **numbers** already present in `ablation_results.json` or in trace exports.

## Two mechanisms I will not forget

**First**, the **prefill/decode** split is the simplest model that makes senior engineers nod: it explains **TTFT**, **KV cache reuse**, and why **prompt engineering** is not morally separate from **systems engineering**. Once you internalize it, you stop asking vague optimization questions and start asking **which phase moved** when something regressed.

**Second**, **paired bootstrap** is a statistical detail that behaves like a **product lever** on fixed eval sets. Positive correlation across methods on the same tasks is not a niche curiosity; it is the default when **lead difficulty** is shared. Ignore covariance and you do not get “conservative science”; you get **misleading uncertainty** that systematically favors **inaction**.

## Public artifacts and teaching

Shipping explainers publicly enforced a **clarity** bar that private notes never did. Writing for a partner is intimate; writing for the internet is **adversarial** in the best sense. The tweet threads were particularly useful as a **compression test**: if the mechanism cannot survive six standalone tweets, the blog probably contained **ornament** instead of **structure**.

The **four** public posts and threads (URLs belong in the repository README per course instructions) mirror the four **asker** questions and four **explainer** rotations described above. Readers may arrive without my portfolio context; the posts therefore **anchor** each mechanism in a class of FDE problems—**serving**, **integration**, **post-training**, and **evaluation**—rather than only in my filenames.

## Closing

Week 12 did not add a new product layer; it **tightened** the evidentiary chain on the layers already shipped. The portfolio still contains the same agent and bench, but the claims those artifacts make are now **partitioned** into the mechanisms that support them—**inference phases**, **decoder constraints**, **adapter capacity**, and **paired uncertainty**—each with a path from **question** to **source** to **edit**. That is the compounding the week promised: **find the gap, sharpen the question, teach what you learned, edit what you already shipped.**
