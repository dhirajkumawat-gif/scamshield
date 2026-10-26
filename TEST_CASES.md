# TEST_CASES.md — Expected vs Observed

Observed values below were produced by running `evaluate_sample_dataset()` (the real scoring functions) on the build machine. Re-run any time on the **Evaluation** page or with `pytest`.

| # | Input | Expected | Observed | Pass / Fail |
|---|---|---|---|---|
| 1 | M1 (message) | LOW 0 | LOW 0 | Pass |
| 2 | M2 (message) | HIGH 85 | HIGH 85 | Pass |
| 3 | M3 (message) | HIGH 50 | HIGH 50 | Pass |
| 4 | M4 (message) | LOW 0 | LOW 0 | Pass |
| 5 | M5 (message) | LOW 0 | LOW 0 | Pass |
| 6 | M6 (message) | HIGH 50 | HIGH 50 | Pass |
| 7 | X1 (transaction) | LOW 0 | LOW 0 | Pass |
| 8 | X2 (transaction) | HIGH 75 | HIGH 75 | Pass |
| 9 | X3 (transaction) | MEDIUM 30 | MEDIUM 30 | Pass |

**Summary:** 9/9 passed (100.0%), false alarms on expected LOW: 0, missed expected HIGH: 0.

> Exercise-set counts on 9 synthetic examples, not validated real-world precision/recall.

## Automated edge-case tests (`backend/tests/test_scoring.py`)

26 test functions cover: the nine official examples, empty/whitespace/too-long messages, OTP mention vs OTP request, non-stacking urgency words, topic words alone, plain link without context, zero/negative baseline, negative amount, NaN/inf/bool/text inputs, exact 1.5x / 3x / 10x boundaries, single highest tier, new-device-only (+25), zero amount, band boundaries (24/25/49/50), 100 cap, safety statement present, feedback record/list/clear, and the evaluation summary.

Status on the build machine: **26/26 scoring tests passed** (run with a minimal stand-in for `pytest.raises` because pytest could not be installed offline there). `tests/test_api.py` (10 tests) and the frontend Vitest tests were written but **not run** in that environment — run them with the commands in the README and record your own results here.
