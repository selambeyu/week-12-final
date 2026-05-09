## Evening 

**What came back**

My peer returned an explainer that walks from what LoRA does to the weights through why low rank is often enough, then ties rank to output style under uncertainty: low rank letting pretrained hedging show through, high rank on few examples risking pattern-matching that reads as overconfidence. We met again and discussed those same topics in conversation—comparing their write-up to what we had sketched in the morning and pressure-testing the rank-versus-data-size story against our ORPO setup. That lines up with how I have been interpreting our critic results and gives a cleaner vocabulary for the next methodology note.

**What I learned or adjusted**

The link between intrinsic dimensionality of fine-tuning updates and choosing `r` relative to dataset size is the piece I will carry into planning the next run (e.g., trying a lower rank on the same 51 pairs and comparing intervals). 