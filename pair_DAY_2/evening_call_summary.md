## Evening Call Summary — Day 2

Topic: **Production patterns — structured output and constrained decoding.**

The asker confirmed the explainer’s core distinction landed: **prompt-only** control reshapes logits but leaves the full vocabulary in play, while **schema- / grammar-constrained decoding** masks illegal next tokens after each prefix so the model samples only valid continuations. The asker asked for one more sentence on **reliability of form vs. judgment** (valid JSON does not imply a correct verdict); that was added before sign-off.

The writer asked whether **streaming partial JSON** and vendor-specific **refusal** behavior should be in scope; both sides agreed those belong in a follow-on note so the day’s post stays focused on the token-level masking story.

The asker revised the judge client README to mention **typed interfaces** for critic outputs and to stop treating “valid JSON” as sufficient evidence of rubric quality.
