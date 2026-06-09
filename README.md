# The Long Tail, Not the Front Page: Cold-Start Prediction of Crowd Highlight Salience

Public reproducibility bundle for the paper. Self-contained and ready to push to a dedicated
public repository.

<!-- arXiv badge: fill in after posting -->
<!-- [![arXiv](https://img.shields.io/badge/arXiv-XXXX.XXXXX-b31b1b.svg)](https://arxiv.org/abs/XXXX.XXXXX) -->

This is the fourth paper in a program on social highlighting, after **Personal Salience**
(`glasp-co/personal-salience`), **Selection, Not Salience** (`glasp-co/personal-selection`), and
**Factions Within, Uncertain Across** (`glasp-co/clone-crowd`). Those study the *individual* or
the *segmented* crowd; this paper predicts the *aggregate* crowd on documents that have no marks
yet (cold start).

## TL;DR

A crowd's highlight map exists only for documents people have already read. We ask whether it can
be predicted from text alone. Off-the-shelf zero-shot LLMs cannot (they lose to a lead/position
baseline), so we train. Findings:

- A logistic ranker over sentence embeddings + positional/contextual features beats lead by
  **+0.044 AP** (95% CI [+0.030, +0.058]; clears the pre-registered margin δ=0.03 in 97% of
  bootstrap resamples), replicated across three separately drawn samples.
- **Two unsupervised extractive baselines (centroid, LexRank-style centrality) lose to lead**; the
  trained model beats them by +0.108 — the edge is learned from real reader marks, not generic
  salience.
- Product-meaningful: **precision@3 rises 0.25 → 0.39**, and the model beats lead on **69%** of
  documents.
- Not a temporal-generalization failure; no evidence of content-drift or near-duplicate leakage
  (removing near-twins *raises* the edge).
- A standardized regression: the advantage is driven by **document popularity** (lower → larger)
  and **label reliability** (thicker crowd labels → larger measured edge). It nearly vanishes
  only on **currently-viral** content — and there it is the **lead baseline that rises**, not the
  model that fails.

The honest scope: evaluation conditions on documents that *eventually* reached ≥20 highlighters,
so this is a retrospective cold-start simulation; within it, day-zero prediction is most feasible
on low-popularity, long-tail documents and least useful on the viral front page that accrues
human marks fastest anyway.

## Results at a glance (advantage over lead = AP(model) − AP(lead); 95% by-document bootstrap CI)

| Result | Value |
| --- | --- |
| M3 − lead (headline) | +0.044 [+0.030, +0.058], clears δ in 97% of resamples |
| embedding effect / augmentation effect | +0.014 [+0.010, +0.019] / +0.010 [+0.002, +0.018] |
| unsupervised centroid / centrality − lead | −0.065 / −0.065 (both lose to lead) |
| precision@3 (lead → M3) | 0.254 → 0.394 (+0.141 [+0.103, +0.180]) |
| de-duplicated / temporal control | +0.053 [+0.035, +0.070] / Δ +0.001 [−0.008, +0.010] |
| regression: popularity / label thickness | β −0.32 [−0.56, −0.14] / +0.22 [+0.07, +0.42] (others n.s.) |

## Contents

- `paper.tex` — the paper (compile with pdflatex / arXiv).
- `paper.pdf` — the compiled paper (10 pages, 3 figures, 4 tables).
- `figures/` — three figures (PDF + PNG): the representation ladder, the per-cell model-vs-lead AP
  decomposition, and the replication + standardized-regression panel.

## Reproducibility

Every effect size carries a 3,000-iteration by-document cluster-bootstrap CI; the model ladder, the
margin δ, and the slice definitions were fixed before running. The data-extraction and scoring
pipeline runs against Glasp's private user data and is **not** released; per-document results derive
from individual highlighting behavior and are not published. The cluster-bootstrap estimator and
aggregate statistics are available to researchers on reasonable request.

## Citation

```bibtex
@misc{nakayashiki2026coldstart,
  title  = {The Long Tail, Not the Front Page: Cold-Start Prediction of
            Crowd Highlight Salience},
  author = {Nakayashiki, Kazuki and Watanabe, Keisuke},
  year   = {2026},
  eprint = {XXXX.XXXXX},
  archivePrefix = {arXiv},
  primaryClass  = {cs.IR}
}
```

<!-- Fill in `eprint` with the arXiv id once the paper is posted. -->

## License

Paper (`paper.tex`, `paper.pdf`) and figures: CC BY 4.0. See `LICENSE`.
