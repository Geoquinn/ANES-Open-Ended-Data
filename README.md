# ANES Open-Ended Data

**A recovered classification of candidate "likes" and "dislikes" from the American National Election Studies.**

Maintained by [George D. Quinn](https://geoquinn.github.io), Department of Political Science, Rutgers University.

---

## Overview

For decades the American National Election Studies (ANES) classified respondents' open-ended candidate "likes" and "dislikes" using a standardized coding structure. Since 2008 the ANES has released these responses **without comparable codes**. That gap severed a fifty-year time series of voters describing candidates in their own words, and with it the ability to ask how the substance of candidate evaluation has changed over time.

This repository provides a **validated, AI-assisted reconstruction** of that coding structure for the post-2008 election years, along with the codebook, validation results, and documentation needed to evaluate and reuse it.

The classification is produced by a human-in-the-loop, API-based workflow that adapts the original ANES codebook into **35 topics nested within 9 major categories**. It is designed to be checked, not trusted: every release ships with held-out validation statistics and per-category error reporting.

## Coverage

| Election year | Status | Responses classified |
|---|---|---|
| 2020 | Released | 16,418 |
| 2024 | Released | *[add N]* |
| 2016 | In development | — |
| 2012 | In development | — |

All covered years fall within the period for which ANES open-end response texts are **publicly downloadable in redacted form** (2008 onward). See [License and Terms of Use](#license-and-terms-of-use) below.

## Repository structure

```
.
├── data/            # Classified response-level and respondent-level files
├── codebook/        # 9 major categories, 35 nested topics, coding rules
├── validation/      # Held-out validation results, human-coder agreement
├── scripts/         # Classification workflow and replication code
└── docs/            # Additional documentation
```

*[Adjust to match your actual directory layout.]*

## Method

The workflow was evaluated in three stages, in this order:

1. **Human benchmark.** Agreement among expert human coders was measured first, to establish a realistic performance ceiling. Model performance is reported against this benchmark, not against an assumption of perfect human reliability.
2. **Calibration.** The model was calibrated through iterative batches of agreed human-coded examples. These examples are *not* used in validation.
3. **Held-out validation.** After the full dataset was classified, results were evaluated against **800 independently coded responses withheld from calibration**.

## Validation results

Performance at the **nine-category level** (2020 held-out sample):

| Metric | Range |
|---|---|
| Micro-F1 | .703 – .798 |
| Respondent-level Cohen's κ | .601 – .752 |

**Known limitations — please read before use:**

- Performance is **strongest for well-defined categories** such as personal qualities and domestic policy.
- Performance **degrades for diffuse, low-frequency categories**, and was weakest for negative evaluations of Donald Trump in the 2020 data.
- The model **assigns more codes per response than human coders**, producing systematically **higher recall than precision**. Users doing prevalence estimation should account for this.
- Reliability is **substantially better at the 9-category level than at the 35-topic level.** Fine-grained topic claims should be treated as provisional and validated against your own use case.

These are not incidental caveats. AI-assisted classification is a measurement strategy requiring human benchmarks, held-out validation, and transparent error reporting — it is not a substitute for human judgment. See `validation/` for full per-category results.

## Suggested use

This database is intended for researchers studying candidate evaluation, campaign communication, negativity and affect in political judgment, and the measurement properties of LLM-based text classification.

Recommended practice:

- Prefer the **9-category** codes for inferential work; use the 35-topic codes for exploratory or descriptive analysis.
- Report the validation statistics above alongside any results derived from these codes.
- Where feasible, hand-code a small sample from your own subset of interest as a local check.

## License and Terms of Use

### The underlying survey data

The open-ended responses classified here originate with the **American National Election Studies**, administered through a collaboration between the University of Michigan and Stanford University with funding from the National Science Foundation. ANES data are not the intellectual property of this project.

ANES treats its public release datasets as public goods and asks that derived work link back to the original dataset. Users of this repository are expected to obtain the source data from ANES directly and to observe the ANES conditions of use, which require that you:

- Use the datasets solely for research or statistical purposes, and **not** to investigate specific survey respondents.
- Make no use of the identity of any respondent discovered intentionally or inadvertently, and report any such discovery to `anes@electionstudies.org`.
- Cite ANES data and documentation in any work that uses them, and send citations of resulting publications to ANES for its bibliography.
- Acknowledge that ANES and its funding agencies bear no responsibility for any use of the data or for interpretations or inferences drawn from it.

Source data: <https://electionstudies.org/data-center/>

### Public vs. restricted open-end texts — important

ANES draws a hard line here, and it determines what this repository can contain:

| Study years | Open-end text status | Redistribution of derivatives |
|---|---|---|
| **2008 and later** | Publicly downloadable in redacted form via the ANES study pages | Permitted, with attribution and a link back to the source study |
| **1996–2004** | **Restricted-Use Data**, available by application through ICPSR's Virtual Data Enclave | **Prohibited** |
| **1984–1992** | Restricted-Use; released unredacted with randomized replacement case IDs | **Prohibited** |
| **Pre-1984** | Transcribed from archived paper questionnaires; availability by inquiry, subject to restricted-use limits | **Prohibited** |

> ⚠️ **ANES restricted-use datasets — and derivatives of them, explicitly including replication datasets — may not be disseminated further.** This is a respondent-confidentiality requirement, not a formality.
>
> In practice: codes derived from **2012–2024** responses can be released here. Codes derived from pre-2008 responses **cannot**, even though those years are central to the associated research. Work extending the classification backward through the historical series stays inside the enclave, with only aggregate results appearing in publications. Keep the two clearly separated in this repository, and confirm that nothing under `data/` was produced from restricted-use inputs before each release.

Restricted-use access details: <https://electionstudies.org/data-center/restricted-data-access/>

### This repository's own contributions

The **codebook adaptation, classification codes, validation results, scripts, and documentation** created by this project are released under *[choose one — e.g. CC BY 4.0 for data and documentation, MIT for code]*.

This license applies **only** to the derived materials produced here. It does not and cannot extend to the underlying ANES survey data, which remain governed by the ANES conditions above. Redistributing this repository grants no rights to the source data.

## Citation

If you use this database, please cite:

> Quinn, George D. 2026. *American National Election Study — Open-Ended Response Database: Candidate Likes and Dislikes.* Department of Political Science, Rutgers University.

And cite the underlying ANES study or studies you used, per ANES policy.

The methodology is described in:

> Quinn, George D., and Richard R. Lau. "Steering AI for Classifying Open-Ended Text: An Evaluation of ANES 2020 Candidate Likes and Dislikes." *Under review.*

*[Update with final publication details once available.]*

## Contact

George D. Quinn — `George.Quinn@rutgers.edu` — [geoquinn.github.io](https://geoquinn.github.io)

Issues and corrections are welcome via the repository issue tracker.
