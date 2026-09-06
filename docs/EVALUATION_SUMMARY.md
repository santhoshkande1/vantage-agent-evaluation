# Results and evidence

Both runs evaluate the existing Vantage agent on the same frozen 40-case synthetic V2 golden set.

| Metric | Baseline | Fresh final | Delta |
| --- | ---: | ---: | ---: |
| Correct handling | 52.5% | 100% | +47.5 percentage points |
| Required facts | 47.5% | 100% | +52.5 percentage points |
| Required evidence | 51.4% | 100% | +48.6 percentage points |
| Mean latency | 5.69 s | 5.67 s | −0.02 s |

Required evidence is scored on 35 applicable cases. The latency difference is not a demonstrated performance improvement.

Baseline cost was not recorded. The final run captures usage and published-price estimates for 38 model-invoking cases; two safe-stop cases are not applicable. Estimated total: **$0.028720**; mean per model-invoking case: **$0.000756**. Neither a billing total nor a cost-saving delta is claimed.

## Review the evidence

- [Evaluation report (Google Doc)](https://docs.google.com/document/d/1-bU63SsVQ9SBxZYcjkDZxO28SpL0amHEzs0U889j38E/edit) — live-document sharing awaits approval.
- [Workbook download](../Vantage%20Agent%20Evaluation%20Workbook.xlsx) — human labels and fresh judge calibration.
- [Public dataset and experiments](https://smith.langchain.com/public/d4be6f7e-27d0-4187-a9d7-528c927a0c9b/d) — compare baseline `3bda5b6e-4e00-409b-81d7-4219d7660f41` with fresh final `92912966-8d68-4b2a-bac3-6c465729635c` (name ending `trace-evidence-7ec4b2f7`).
- [Public V2-PROC-010 trace](https://smith.langchain.com/public/5d0f3999-fe9c-4d8b-98df-3796ef092481/r/01a0781e-e56f-7691-b237-0acfcdc3e620?start_time=2026-09-06T19%3A08%3A05.871067Z) — case ID, inputs/output, parent/child runs, timing, and tokens.
- [Baseline CSV](../results_v1.csv) and [final CSV](../results_v2.csv) — direct LangSmith SDK exports, 40 matched case IDs each; the README explains columns, missing values, and metric definitions.
- [Actual comparison screenshot](evidence/evaluation/langsmith-comparison.png) and [actual trace screenshot](evidence/evaluation/langsmith-trace.png) — original-resolution UI captures. A is final; B is baseline. Complete answer text remains in the CSVs.

The [improvement record](IMPROVEMENT_EVIDENCE.md) describes three agent changes and one observability change. Outcomes are cumulative, not isolated ablations. Perfect scores on this development set do not establish generalization, independent-judge answer quality, or production readiness.

Implementation and tests remain in the separate Vantage development project. This repository contains assignment artifacts only; no local code execution or notebook is included.

The main observed remaining weakness is the broad assessment (V2-PORT-001): 64.796 seconds, 44 model calls, and $0.009490 estimated cost. All-green route/claim/tool checks do not eliminate latency, cost, semantic-faithfulness, or generalization limitations. The project owner confirms completing human review of the golden set; the fraction of LLM-generated questions remains unconfirmed. The 21 human failure-category labels are a separate calibration artifact.
