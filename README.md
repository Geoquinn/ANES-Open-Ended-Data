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

## Data source and terms of use

The underlying open-ended responses are the property of the **American National Election Studies** and are subject to ANES terms of use. Users of this repository must independently obtain the source data from the ANES and comply with those terms, including:

- Use solely for research or statistical purposes, and not for investigation of specific respondents.
- No use of the identity of any respondent discovered intentionally or inadvertently; report any such discovery to `anes@electionstudies.org`.
- Cite ANES data and documentation in any work using them.

The original collectors of the data, the ANES, and its funding agencies bear no responsibility for the analyses or interpretations presented here. <a href="https://electionstudies.org/data-center/">Visit W3Schools.com!</a>


## Citation

If you use this database, please cite:

> Quinn, George D. 2026. *American National Election Study — Open-Ended Response Database: Candidate Likes and Dislikes.* Department of Political Science, Rutgers University.

The methodology is described in:

> Quinn, George D., and Richard R. Lau. "Steering AI for Classifying Open-Ended Text: An Evaluation of ANES 2020 Candidate Likes and Dislikes." *Under review.*

*[Update with final publication details once available.]*

## License

*[Specify — e.g. CC BY 4.0 for the derived codes and documentation, noting that the underlying ANES data carry their own terms.]*

## Contact

George D. Quinn — `George.Quinn@rutgers.edu` — [geoquinn.github.io](https://geoquinn.github.io)

Issues and corrections are welcome via the repository issue tracker.
