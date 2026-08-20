# DialectGuard-Robustness-Evaluation-of-Arabic-AI-Generated-Text-Detectors

This repository contains **AraDeed**, an Arabic AI-generated text (AIGT) detection
dataset, together with four adversarial test variants and the code accompanying the
paper *"DialectGuard: Robustness Evaluation of Arabic AI-Generated Text Detectors
Against Dialectal and Adversarial Attacks."*

## Overview

AraDeed is a balanced dataset of 10,000 samples for distinguishing human-authored
from machine-generated Arabic text:

- **5,000 human-authored** articles drawn from the SANAD Arabic news corpus
- **5,000 machine-generated** texts produced by prompting LLaMA-3.1 (via the Groq API)
  to rephrase the corresponding human articles

The dataset targets two under-studied dimensions of Arabic AIGT detection:
adversarial robustness and dialectal perturbation.

## Repository contents

| File | Description |
|------|-------------|
| `AraDeed_final.csv` | Full dataset: 10,000 labelled samples (`text`, `label`) |
| `test_clean.csv` | Held-out clean test split |
| `test_attack1_paraphrase.csv` | Test set under paraphrase attack |
| `test_attack2_backtrans.csv` | Test set under back-translation attack |
| `test_attack3_dialect.csv` | Test set under MSA→Egyptian dialect substitution |
| `test_attack4_worddrop.csv` | Test set under word-drop perturbation |
| `DialectGuard.ipynb` | Full pipeline: data prep, fine-tuning, attacks, evaluation |

## Data format

Each CSV has two columns:

- `text` — the Arabic text sample
- `label` — `0` for human-authored, `1` for machine-generated

## Labels and splits

The dataset is balanced (50% human / 50% machine) and split 70/15/15 into
train / validation / test, stratified by label.

## Adversarial variants

Four attacks are applied **to the machine-generated samples** of the test set,
producing the four `test_attack*.csv` files. Human samples are left unchanged.

1. **Paraphrase** — regeneration in a different style via LLaMA-3.1
2. **Back-translation** — Arabic → English → Arabic
3. **Dialect substitution** — MSA replaced with Egyptian Arabic equivalents
4. **Word-drop** — random token removal at a 30% rate

## Models evaluated

Three Arabic pre-trained transformers are fine-tuned as detectors:
AraBERT, MARBERT, and AraELECTRA. Results are reported as mean ± standard deviation
over three random seeds (42, 1337, 2024).

## Source corpus and licensing

The human-authored half of AraDeed is derived from the **SANAD** corpus.
Users of this dataset should consult and comply with the original SANAD license and
cite the SANAD dataset in addition to this work.
<!-- TODO: confirm SANAD redistribution terms and adjust this section accordingly -->

## Citation

If you use AraDeed or this code, please cite:
