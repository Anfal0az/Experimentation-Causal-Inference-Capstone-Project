# Smart Reminder Experiment — Injaz Capstone

**Capstone project for the *Experimentation & Causal Inference* program at [SDAIA Academy](https://github.com/SDAIAAcademy).**

## Overview

This capstone asks: should **Injaz** — a fictional, synthetic Saudi digital-government
services platform used for teaching purposes — launch a **"smart reminder"** (a push
notification / SMS nudge sent partway through a user's session) to help users finish the
online service they started?

The notebook works through the full decision end-to-end:

1. **Why you can't just launch it and compare before/after.** A simulated opt-in / self-selection
   design shows how a naive before/after comparison is biased by confounding — users who opt in
   are already more likely to finish, reminder or not.
2. **Design, simulate, and correctly analyze a randomized experiment.** A proper power/MDE/sample-size
   plan, an A/A pipeline sanity check, a two-proportion test on the primary metric, a CUPED-adjusted
   guardrail metric, and a demonstration of how naive "peeking" inflates false positives (fixed with
   an always-valid mixture-SPRT boundary).
3. **Read the result honestly.** Full covariate-balance diagnostics, a permutation-test robustness
   check, an E-value sensitivity analysis, multiple-comparison and subgroup-fishing illustrations,
   and an explicit design-credibility checklist (sample-ratio mismatch, interference, novelty
   effects, generalizability).
4. **The decision memo.** A one-page recommendation to the product lead, stating the primary result,
   the guardrail result, the key threats to the conclusion, and why the earlier naive estimate
   would have been the wrong number to trust.

## Contents

| File | Description |
|---|---|
| `Capstone_Smart_Reminder.ipynb` | The full analysis notebook (causal design, simulation, estimation, diagnostics, sensitivity analysis, and decision memo). |
| `injaz_users.csv` | The synthetic Injaz user pool used throughout the notebook. |
| `Smart_Reminder_Decision_Memo.docx` | The standalone two-page decision memo for the product lead (recommendation, results, DAG, threats, and next steps). |
| `dag_smart_reminder.png` | The causal DAG for the smart reminder's identification strategy, also embedded in the notebook and the memo. |

## Data

`injaz_users.csv` is **100% synthetic** — no real citizen, government record, or personal data
is used anywhere in this project. It was generated for teaching purposes as part of the
SDAIA Academy curriculum. The notebook's data dictionary (in its own markdown cells) documents
every column.

## Method summary

- **Design:** Completely randomized experiment (A/B test), not an observational adjustment —
  chosen because Injaz can assign the reminder directly rather than relying on who happens to
  select into it.
- **Estimand:** Average Treatment Effect of the reminder on the probability a user completes the
  service session they started, for the population of Injaz users starting an online session.
- **Diagnostics:** Standardized mean difference (SMD) covariate balance, sample-ratio mismatch
  (SRM) check, A/A test, Fisher's randomization (permutation) test.
- **Inference:** Neyman design-based standard errors, two-proportion z-test, CUPED variance
  reduction for the guardrail metric, an always-valid (mixture-SPRT) sequential testing boundary.
- **Sensitivity analysis:** E-values computed for both the randomized estimate and the discarded
  self-selected estimate, to quantify how much unmeasured confounding each would require.

## Requirements

- Python 3.9+
- `numpy`, `pandas`, `matplotlib`, `scipy`

```bash
pip install numpy pandas matplotlib scipy
```

## Running the notebook

```bash
jupyter notebook Capstone_Smart_Reminder.ipynb
```

Run all cells top to bottom (`Kernel → Restart & Run All`). Random seeds are fixed throughout so
results are reproducible.

> **Note:** the data-loading cell reads `injaz_users.csv` from a shared Google Drive link by
> default. If you don't have internet access in your runtime, point that cell at the local
> `injaz_users.csv` file included in this repo instead.

## Acknowledgments

This project was completed as part of the **Experimentation & Causal Inference** track at
[SDAIA Academy](https://github.com/SDAIAAcademy). The Injaz dataset and lab materials
(potential-outcomes simulation, A/B testing pipeline) referenced throughout the notebook are
part of that program's curriculum.

## License

This project is licensed under the terms of the [MIT License](LICENSE).
