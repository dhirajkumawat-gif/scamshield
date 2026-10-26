# 3-Minute Demo Script — ScamShield AI (H05)

Team name: ______  Members: ______

| Time | Do | Say |
|---|---|---|
| 0:00–0:30 | Overview page | People get pressure messages and odd payment alerts and can't tell real from fake. ScamShield explains *why* something looks risky and what to do next. |
| 0:30–1:00 | Sample Lab → M2 → Load → Analyze | 85/100 HIGH: urgency +25, credential request +35, suspicious link +25. The link was never opened. |
| 1:00–1:20 | Load M5 | LOW, 0. It mentions a one-time code but only warns "do not share" — we detect *requests*, not keywords. |
| 1:20–1:45 | Transaction Checker → X2 | ₹48,000 vs ₹700 baseline is 68.57x → +50; new device +25; total 75 HIGH. |
| 1:45–2:15 | Evaluation page | 9 examples run through the real code. Expected vs observed, PASS/FAIL, false alarms 0, missed HIGH 0. |
| 2:15–2:40 | Press Useful on a result; show Feedback page; point to safe steps and "A risk flag is not proof of fraud." | Feedback is recorded in memory only. |
| 2:40–3:00 | About page | Measured: 9 synthetic examples only. Not measured: real fraud reduction. Next step: more languages and a labelled test set. |

## Likely judge questions
- **Why rules, not ML?** Transparent, explainable, works offline, no training data needed; every point is traceable.
- **False positives?** A legitimate message with a verify link can be flagged; that's why we say "not proof" and give verification steps. Run your own organizer case live.
- **How do you avoid flagging M5?** Credential rule needs a request verb near a sensitive term and skips negated sentences ("do not share").
- **Privacy?** No external calls, message text never stored/logged/returned, feedback stores no message text.
- **Why no bank integration?** Out of scope and unsafe for a hackathon; the tool only advises.
- **Is 100% on 9 examples meaningful?** No; rules were built with those examples in view. It's a sanity check, not accuracy.
