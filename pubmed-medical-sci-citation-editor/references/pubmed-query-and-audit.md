# PubMed Query And Audit Reference

Use this file when the task needs detailed PubMed query construction, evidence filters, or audit math.

## Query Construction Principles

- Start with the claim, not the disease area.
- Combine topic terms with the exact outcome, mechanism, biomarker, intervention, or population mentioned in the sentence.
- Add study-design filters when evidence hierarchy matters.
- Add publication-date filters directly in the query whenever possible.
- Prefer title and abstract fielding for precision:
  `"keyword"[Title/Abstract]`

## Recency Filters

Primary target window:

```text
("2016/01/01"[Date - Publication] : "3000"[Date - Publication])
```

Five-year target window:

```text
("2021/01/01"[Date - Publication] : "3000"[Date - Publication])
```

Fallback window when recent literature is insufficient:

```text
("2011/01/01"[Date - Publication] : "2015/12/31"[Date - Publication])
```

Do not accept anything before `2011/01/01`.

## Common Query Templates

### Disease Background Or Burden

```text
("disease name"[Title/Abstract]) AND ("incidence" OR "prevalence" OR "mortality" OR "burden") AND ("2021/01/01"[Date - Publication] : "3000"[Date - Publication])
```

### Mechanism

```text
("disease name"[Title/Abstract]) AND ("pathway" OR "mechanism" OR "signaling" OR "immune microenvironment") AND ("2021/01/01"[Date - Publication] : "3000"[Date - Publication])
```

### Biomarker Or Diagnostic Claim

```text
("biomarker"[Title/Abstract]) AND ("disease name"[Title/Abstract]) AND ("diagnosis" OR "prognosis" OR "predictive value") AND ("cohort" OR "validation" OR "prospective") AND ("2016/01/01"[Date - Publication] : "3000"[Date - Publication])
```

### Treatment Effect

```text
("disease name"[Title/Abstract]) AND ("therapy name"[Title/Abstract]) AND ("randomized" OR "trial" OR "phase 3" OR "meta-analysis") AND ("2016/01/01"[Date - Publication] : "3000"[Date - Publication])
```

### Methods

```text
("assay or method name"[Title/Abstract]) AND ("protocol" OR "guideline" OR "standard") AND ("2011/01/01"[Date - Publication] : "3000"[Date - Publication])
```

## Evidence Hierarchy Hints

Prefer, in order:

1. Meta-analysis or systematic review
2. Randomized controlled trial
3. Prospective multicenter cohort
4. Large retrospective cohort or registry
5. High-quality mechanistic or translational study when the claim is mechanistic
6. Official guideline, consensus statement, or kit/protocol paper when Methods support is needed

## Citation Mapping Rules

- Use 1 citation when one paper fully supports the claim.
- Use 2 citations only when they add distinct dimensions.
- Use 3 citations only when each one is necessary and non-overlapping.
- Avoid stacking three papers from the same study type, population, or conclusion unless the sentence itself is comparative.

Examples of complementary grouping:

- Mechanistic cell or animal evidence plus human clinical cohort evidence
- Discovery cohort plus external validation cohort
- Guideline or method paper plus application paper

## Audit Math

Let:

- `R` = total unique references
- `V` = references verified with PubMed
- `Y5` = references from 2021-2026
- `Y10` = references from 2016-2026
- `I_D` = number of citation placements in Introduction plus Discussion
- `C_all` = total citation placements across all sections
- `S1` = references cited exactly once
- `M` = maximum citations used at one insertion point

Compute:

- PubMed verification rate = `V / R`
- Five-year rate = `Y5 / R`
- Ten-year rate = `Y10 / R`
- Intro/Discussion placement rate = `I_D / C_all`
- Single-use rate = `S1 / R`

Target thresholds:

- `V = R`
- `Y5 / R >= 0.70`
- `Y10 / R >= 0.90`, with all remaining older references still after 2010
- `I_D / C_all >= 0.80`
- `S1 / R >= 0.70`
- `M <= 3`

## Failure Handling

- If a metric fails, revise the citation map first rather than editing the audit text.
- If the newest high-level evidence is not a direct fit, prefer a recent high-quality primary study over an older broad review.
- If no eligible paper exists within the date rules, narrow or rewrite the claim and then search again.
