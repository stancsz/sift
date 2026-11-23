# Sift: market position and maturity

**Reviewed:** 2026-11-23<br>
**Product readiness:** public pre-release / research prototype. A standalone CLI and LiteLLM callback are available; broader coding-agent acceptance and quality parity are not established.<br>
**Market validation:** hypothesis with a small public visibility signal. Active adoption and willingness to pay are unknown.

## Audience and job

The intended user is a developer or researcher running long coding-agent sessions whose accumulated history makes later requests large or hard to navigate. The job is to select older, task-relevant excerpts within an explicit request budget while keeping recent work exact and refusing safely when protected current work cannot fit.

## Alternatives and position

| Substitute | What its first-party source establishes | Sift's testable position |
| --- | --- | --- |
| Server-side conversation compaction | OpenAI's Responses API can compact a conversation on the server as a context-management operation. | Sift is a local pre-call selector with explicit recency and source-preservation rules. It should be compared on task quality, latency, compatibility, and cost, not token reduction alone. |
| Learned prompt compression | LongLLMLingua studies model-based prompt compression and reports benchmark-specific results. | Sift's current selector makes no summary-model call. Whether deterministic selection is more useful for coding histories is unproven. |
| Larger context windows or shorter sessions | Simple operational choices that avoid adding a compactor. | Sift is useful only when users prefer a smaller working context and measured quality loss is acceptable. |

Sources: [OpenAI context compaction](https://developers.openai.com/api/docs/guides/compaction) and [LongLLMLingua](https://arxiv.org/abs/2310.06839). These sources are not head-to-head Sift comparisons.

## Evidence and limits

- In the broader exposed LongBench v2 cohort, 343 paired clusters had three repeats per arm. Sift used 59.66% fewer prompt tokens and scored 5.25 percentage points lower on task-majority than Full context; the reported 95% cluster-bootstrap interval was −10.20 to −0.29 pp.
- Public questions were exposed during development. This is not a blind holdout, a coding-agent success study, or evidence of preserved task quality.
- A separate synthetic 950K-token request probe estimated 32.7K–37K forwarded tokens for one request per model. Its API-rate-equivalent comparison is not measured subscription savings or quality parity.
- GitHub snapshot on 2026-11-23: 1 star, 0 forks, and pre-release `v0.11.1`. These signals do not establish active use or retention.

## Adoption friction and next experiment

Compression can remove necessary context, token counts vary across protocols, and callback integration changes request handling. The next decision-changing study is a blind, held-out set of coding-agent histories with identical task, model, tools, and budget across Full and Sift conditions. Independently grade completion, correctness, regressions, and recovery; record full provider receipts and the source excerpts retained. Predeclare a non-inferiority margin before opening outcomes.

## Product and research values

- **Preserve active work:** protected current content is not silently discarded to hit a target.
- **Keep selection inspectable:** deterministic rules and receipts expose why material was kept.
- **Fail closed:** oversized protected requests remain explicit failures.
- **Report the trade-off:** prompt-token reduction and task quality appear together.

## Sources

- [Project README](../README.md)
- [Evaluation protocol and limits](evaluation.md)
- [Algorithm](algorithm.md)
- [OpenAI context compaction](https://developers.openai.com/api/docs/guides/compaction)
- [LongLLMLingua paper](https://arxiv.org/abs/2310.06839)
