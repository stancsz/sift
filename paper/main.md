# Selective Context Retention for Long-History Language Model Requests

A paired LongBench study of task-majority quality and prompt-token use

## Abstract

Sift deterministically selects context from coding-agent histories. It preserves the active request and recent tool work when they fit, selects older task-related excerpts within a budget, and fails closed if protected current work cannot fit. It does not make a summary-model call. In a repository-reported study on an exposed 344-question LongBench cohort, one Full-context HTTP 529 was not retried, leaving 343 paired question clusters. Full context achieved task-majority on 145 of 343 questions and Sift on 127 of 343: a difference of -5.25 percentage points (cluster-bootstrap 95% CI -10.20 to -0.29). Sift used 59.66% fewer provider prompt tokens. This is not blind evidence or coding-agent task success.

## 1. Motivation and method

LongBench [R1] measures long-context understanding; tool histories can also exceed a model's practical context budget. Full history retains irrelevant material, while model summarization can alter details and adds another model call. Sift selects older excerpts deterministically while preserving the active request and protected recent work when they fit.

If protected work cannot fit, Sift fails closed rather than silently discarding the current task. The evaluation compares Full context and Sift under the repository's documented request construction, token accounting, model, and answer-scoring procedure.

## 2. Results

The repository study record [R2] reports an assigned cohort of 344 questions. One Full-context request received HTTP 529 and was not retried, leaving 343 paired clusters. Full context achieved task-majority on 145/343; Sift on 127/343. The paired difference was -5.25 percentage points, with repository-reported cluster-bootstrap 95% CI from -10.20 to -0.29.

Sift reduced provider prompt tokens by 59.66% under the study's accounting. A separate repeat evaluation has different counts and is not merged into the primary result.

## Product and research values

Sift preserves the active request and recent tool work, selects older task-related excerpts within a budget, and fails closed when current work cannot fit.

- **Current-task preservation:** protected work is not silently dropped to satisfy a token target.
- **No generated summary step:** selection is deterministic.
- **Measured trade-off:** on the exposed 343-question paired cohort, Sift used 59.66% fewer prompt tokens and scored 5.25 points lower on task-majority than Full context.
- **Limits remain visible:** this is not blind evidence or coding-agent success evidence; broad agent quality is not established.

## 3. Limitations and future work

LongBench does not represent all tool-heavy software development. Task-majority is not independently verified answer correctness for every downstream use. Token savings alone do not establish lower total cost if retries or corrections differ.

Next evaluate held-out repository tasks and real tool traces with matched models and generation settings, report every failure, and measure task acceptance, regressions, correction time, tokens, latency, and overflow behavior.

## 4. Conclusion

On this exposed cohort, Sift used fewer prompt tokens while scoring lower than Full context on the primary task-majority comparison. This is a bounded quality/token trade-off; agent-history utility remains open.

## References

[R1] Bai, Y., et al. LongBench: A Bilingual, Multitask Benchmark for Long Context Understanding. ACL 2024. URL: https://aclanthology.org/2024.acl-long.172/
[R2] Chen, S. Sift repository and LongBench study records. URL: https://github.com/stancsz/sift