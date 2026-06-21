# Community Pulse — Minimal Dataset and Reproducibility Code

This repository accompanies the manuscript:

> **"Enduring Disparities in the Workplace: A Pilot Study in the AI Community"**  
> Yunusa Simpa Abdulsalam, Siobhan Mackenzie Hall, Ana Quintero-Ossa, William Agnew,
> Carla Muntean, Sarah Tan, Ashley Heady, Savannah Thais, Jessica Schrouff  
> 2025. https://arxiv.org/abs/2506.04305

---

## Repository contents

| File | Description |
|---|---|
| `community_pulse_minimal_dataset.xlsx` | Minimal anonymised dataset |
| `community_pulse_reproducibility.ipynb` | Reproducibility notebook |
| `README.md` | This file |

---

## Dataset description

### What this dataset is

`community_pulse_minimal_dataset.xlsx` is the minimal dataset that respects the IRB-approved research protocol
(Columbia University, Protocol IRB-AAAU9608, Exempt determination). The protocol
commits to using only aggregated group data in publications and to GDPR compliance.
No individual-level data are included.

### Sheet structure

The workbook contains **10 data sheets**:

**Per-demographic sheets (7):**
`Gender` · `Age` · `Race_Ethnicity` · `Sexual_Orientation` · `Disability` · `Employer_Type` · `Seniority`

Each column is named `"Survey item (truncated)… | Demographic group"` and contains
the responses for that item × group combination. Values are **independently shuffled**
per column — this means:

- Row positions carry no information; no two columns share the same row order
- Cross-question linkage across columns is impossible (re-identification prevention)
- `value_counts()` for any column is **identical** to the original data (shuffling preserves marginal distributions)
- All statistical analyses that depend only on marginal distributions — chi-squared tests, Mann-Whitney U, fraction-of-unfavourable calculations — are **fully reproducible** and give numerically identical results to the original analysis

Groups with fewer than 30 responses are suppressed (not included), consistent with the study's pre-specified n ≥ 30 reporting threshold.

**Pre-aggregated figure data sheets (3):**

| Sheet | Contents |
|---|---|
| `Figure_4_Intersectional` | Median and IQR of unfavourable fraction by race × gender |
| `Figure_5_Accessibility` | Response-category proportions per accessibility item |
| `Figure_6_Microaggressions` | Proportion who experienced each microaggression type, by minority group |

These sheets contain pre-aggregated statistics derived from the original data and
can be plotted directly to reproduce Figures 4, 5, and 6 of the manuscript.

**README sheet:** column-naming convention, scale coding, privacy measures.

### Scale coding

| Scale | Values | Coding |
|---|---|---|
| Likert (4-point) | 1 · 2 · 3 · 4 | 1 = Strongly agree → 4 = Strongly disagree |
| Frequency (5-point) | 1 · 2 · 3 · 4 · 5 | 1 = Never → 5 = Multiple times/day |

Lower scores indicate more favourable workplace experiences. An **unfavourable
response** is defined as score ≥ 3 on the Likert scale, or score ≥ 2 on the
frequency scale (experienced at least once).

---

## Reproducibility notebook

`community_pulse_reproducibility.ipynb` runs end-to-end using only
`community_pulse_minimal_dataset.xlsx` as its data source. It reproduces:

- Fraction of unfavourable responses per item and per demographic group (Figures 3, 11–13)
- Chi-squared tests with Holm-Bonferroni correction and Cramér's V effect sizes:
  DEI-related leaving intention × demographics, and microaggression frequency × demographics
- Mann-Whitney U tests for disability comparisons (performance fairness; microaggression frequency)
- Figures 4, 5, and 6 plotted from the pre-aggregated summary sheets

The notebook clearly documents which analyses **cannot** be reproduced from this
dataset (paired Wilcoxon for within-respondent comparisons, Cronbach's alpha,
employer-specific comparisons) and explains why.

### Requirements

```
python >= 3.9
pandas
numpy
scipy
statsmodels
matplotlib
openpyxl
```

Install with:

```bash
pip install pandas numpy scipy statsmodels matplotlib openpyxl
```

### Running the notebook

```bash
git clone <repository-url>
cd community-pulse
jupyter notebook community_pulse_reproducibility.ipynb
```

Place `community_pulse_minimal_dataset.xlsx` in the same directory as the notebook before running.

---

## Ethics and data availability

This study was conducted under Columbia University Exempt determination
(Protocol IRB-AAAU9608, approved 15 November 2023). Participation was voluntary
and fully anonymous. No identifiable information was collected.

The raw survey data cannot be released publicly. The approved research protocol
explicitly commits that "any reports or publications based on this research will
use only group data and will not link or identify any human subject." The minimal
dataset in this repository fulfils this commitment by providing only aggregated,
shuffled, threshold-suppressed response distributions.

It is prohibited to attempt to re-identify any participant in this study.

---

## Citation

If you use this dataset or code, please cite:

> Abdulsalam YS, Hall SM, Quintero-Ossa A, Agnew W, Muntean C, Tan S, Heady A,
> Thais S, Schrouff J. Enduring Disparities in the Workplace: A Pilot Study in
> the AI Community. [arxiv](https://arxiv.org/abs/2506.04305) 2026.

---

## License

The code in this repository is released under **Apache 2.0**.  
The minimal dataset is released under **CC BY SA NC 4.0** (Creative Commons Attribution 4.0, share alike, non-commercial).

---

## Contact

For questions about the study or data access requests, contact:  
simpa@blackinai.org · jessicaschrouff@wimlworkshop.org
