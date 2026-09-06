# Targeted improvements and measured evidence

The existing agent received three behavior changes and one observability change. The final measurement is a fresh 40-case evaluation on the frozen V2 dataset, not copied outputs from an older experiment.

| Change | What changed and why | Measured evidence |
| --- | --- | --- |
| Natural-language routing | Recognize everyday wording such as “tech,” “POs,” “go over budget,” and “which apps” within the approved scope. | Eight targeted baseline failures pass: V2-CTX-001, V2-DEP-FIN-001, V2-DEP-IT-001, V2-FIN-004, V2-IT-001, V2-IT-006, V2-PORT-001, V2-PROC-006. |
| Follow-up context recovery | Resolve references to prior contracts, vendors, findings, evidence, and calculations; clarify ambiguous references. | Eight targeted baseline failures pass: V2-FUP-001, V2-FUP-002, V2-PROC-003, V2-PROC-004, V2-PROC-008, V2-PROC-009, V2-PROC-010, V2-PROC-014. |
| Evidence and safety alignment | Use the matching evidence lookup, bind document retrieval to the resolved vendor, require contract/human validation, and stop workforce-reduction requests before tool calls. | Five targeted baseline failures pass: V2-PROC-007, V2-IT-003, V2-IT-004, V2-IT-005, V2-OOS-001. V2-DOC-001 is an extra regression guard, not a sixth baseline failure. |
| Token and cost observability | Capture usage and estimate cost only when pricing is available; distinguish unavailable data from zero cost. | All 40 cases have explicit status: 38 with model usage/cost estimates and two safe-stop cases marked not applicable. No baseline cost-saving delta is available. |

These groups address different checks and must not be summed as a count of distinct correct-handling failures. They were measured together, **not as isolated causal effects**.

## Verification

In the [public V2 dataset](https://smith.langchain.com/public/d4be6f7e-27d0-4187-a9d7-528c927a0c9b/d), compare baseline `3bda5b6e-4e00-409b-81d7-4219d7660f41` with fresh final `92912966-8d68-4b2a-bac3-6c465729635c` (name ending `trace-evidence-7ec4b2f7`). Use the case IDs above to inspect expected outcomes, actual answers, and evaluator feedback.

## Next experiment

Replay one change at a time on the same frozen set to isolate contribution and regressions. Then test unseen paraphrases and ambiguous follow-ups on a held-out set. Current 100% development-set scores justify stronger testing, not a claim that no failures remain.
