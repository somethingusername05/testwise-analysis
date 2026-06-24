# Test-Wiseness in Multiple-Choice Questions

**Can you pick the right answer without reading the question?**

An empirical analysis of **124,096 real exam questions** testing whether surface cues in the wording of answer choices leak the correct option — with the question completely hidden.

![Dashboard Preview](preview.png)

## What this is

Multiple-choice exams assume that a student who doesn't know the answer is reduced to guessing. But what if the way the answers are *written* gives the game away?

This project hides every question and tries to identify the correct answer using only simple tricks on the answer choices: pick the longest, avoid "always/never" words, prefer "usually/often" words, and more. It then measures how far above random guessing each trick can go.

## Key findings

| Finding | Result |
|---|---|
| Random guessing baseline | ~25% |
| Best single trick (pick the longest) | **29%** |
| "All of the above" when present | **70%** correct |
| "None of the above" when present | 18% — a trap |
| All tricks combined (logistic regression) | **29%** — no better than the best single trick |
| Leakiest subject | International Law (+28pp above guessing) |
| Tightest subject | Public Relations (−8pp below guessing) |
| Sanity check (shuffled keys) | Everything collapses to ~25% ✅ |

Most exam questions are well-written. But a small fraction leak the answer through wording — mainly because the correct option tends to be longer and more qualified.

## Data sources

All questions have 5 answer choices or fewer. No question text is included in the analysis — only the answer options.

| Source | Questions | Choices | What it is |
|---|---|---|---|
| [MMLU](https://huggingface.co/datasets/cais/mmlu) | ~16k | 4 | University-level academic exams across 57 subjects |
| [AGIEval](https://github.com/ruixiangcui/AGIEval) | ~2.3k | 4–5 | SAT, LSAT, AQuA-RAT math, LogiQA civil service |
| [RACE](https://huggingface.co/datasets/ehovy/race) | ~88k | 4 | English reading comprehension exams |
| [ARC](https://huggingface.co/datasets/allenai/ai2_arc) | ~7.8k | 4 | Science exams (Challenge + Easy) |
| [CommonsenseQA](https://huggingface.co/datasets/tau/commonsense_qa) | ~9.7k | 5 | Commonsense reasoning |

## Deliverables

| File | Description |
|---|---|
| `testwise_dataset.xlsx` | Raw dataset — 124,096 questions with options A–E and the correct letter |
| `testwise_analysis.ipynb` | Jupyter notebook — full analysis with charts and plain-language explanations |
| `testwise_dashboard.html` | Interactive dashboard — open in any browser, no install needed |
| `testwise_report.docx` | Research report — 7-page Word document with embedded figures |

## How to use

**Dashboard** — just open `testwise_dashboard.html` in your browser. Everything is self-contained (Chart.js is inlined, no CDN).

**Notebook** — place `testwise_dataset.xlsx` in the same folder, then:

```bash
pip install pandas numpy matplotlib scikit-learn wordfreq openpyxl
jupyter notebook testwise_analysis.ipynb
```

**Report** — open `testwise_report.docx` in Word, Google Docs, or LibreOffice.

## Tricks tested

1. **Pick the longest answer** — choose the option with the most characters
2. **Pick the shortest answer** — the opposite
3. **Pick the odd one out** — the option least similar to the others (by word overlap)
4. **Pick the most similar** — the option most like the others
5. **Avoid "always/never"** — dodge options with absolute words
6. **Prefer "usually/often"** — favour options with hedging words

Plus a **combined logistic regression** model stacking all features, validated with grouped 5-fold cross-validation (all options of a question kept in one fold).

## Built with

Python · pandas · scikit-learn · matplotlib · Chart.js · docx

## References

- Haladyna & Downing (1989). A taxonomy of multiple-choice item-writing rules.
- Haladyna, Downing & Rodriguez (2002). A review of MC item-writing guidelines.
- Hendrycks et al. (2021). Measuring Massive Multitask Language Understanding (MMLU).
- Zhong et al. (2023). AGIEval. arXiv 2304.06364.
- Lai et al. (2017). RACE: Large-scale ReAding Comprehension Dataset. EMNLP.
- Clark et al. (2018). Think you have Solved Question Answering? Try ARC. arXiv 1803.05457.
- Talmor et al. (2019). CommonsenseQA. NAACL-HLT.

## License

MIT
