# Test-Wiseness in Multiple-Choice Questions

**Can you pick the right answer without reading the question?**

An empirical analysis of **124,096 real exam questions** testing whether surface cues in the wording of answer choices leak the correct option — with the question completely hidden.

**[▶ View the live dashboard](https://somethingusername05.github.io/testwise-analysis/testwise_dashboard.html)**

## What this is

Multiple-choice exams assume that a student who doesn't know the answer is reduced to guessing. But what if the way the answers are *written* gives the game away?

This project hides every question and tries to identify the correct answer using only simple tricks on the answer choices: pick the longest, avoid "always/never" words, prefer "usually/often" words, and more.

## Key findings

| Finding | Result |
|---|---|
| Random guessing baseline | ~25% |
| Best single trick (pick the longest) | **29%** |
| "All of the above" when present | **70%** correct |
| "None of the above" when present | 18% — a trap |
| All tricks combined | **29%** — no better than the best single trick |
| Leakiest subject | International Law (+28pp above guessing) |
| Sanity check (shuffled keys) | Everything collapses to ~25% ✅ |

Most questions are well-written. But a small fraction leak the answer through wording — mainly because the correct option tends to be longer.

## Data sources

| Source | Questions | What it is |
|---|---|---|
| MMLU | ~16k | University-level exams, 57 subjects |
| AGIEval | ~2.3k | SAT, LSAT, AQuA-RAT, LogiQA |
| RACE |
