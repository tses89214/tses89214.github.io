+++
title = 'Stark Support Bot: Guardrails and Evaluation for an LLM Support Bot'
date = '2026-10-27'
draft = false
description = 'Measuring how well layered defenses block prompt injection in an LLM customer-service bot, starting from the worst baseline and adding one defense at a time.'
tags = ['LLM', 'RAG', 'Evaluation', 'Guardrails']
+++

**The question:** each time a defense is added, how many more attacks does it block? Measured with fixed test cases, not by feel.

**Approach:** a RAG customer-service bot over fictional product docs. I start from a defenseless bot (L0), add one defense at a time, and re-run the same 28 attacks and 6 normal questions after each step.

| Level | Adds | Attacks blocked (95% interval) | Normal questions answered |
|---|---|---|---|
| L0 | nothing: all docs stuffed in a bare prompt | 16 / 28 (44–69%) | 6 / 6 |
| L1 | answer rules ("answer only from the docs") | 22 / 28 (66–87%) | 6 / 6 |
| L2 | input fence + untrusted-input rule | 24.5 / 28 (76–94%) | 6 / 6 |
| L3 | input classifier and routing | 28 / 28 (94–100%) | 6 / 6 |

(Mean of 2 runs per level, one free model.)

**What I care about in the method**
- No LLM judge: attacks are scored by canary strings and doc facts. Deterministic and free, but blunt.
- Small samples always come with confidence intervals; a one- or two-attack difference is treated as noise, so I do not rank individual steps by size.
- 143 labelled classifier cases (57 hand-written, 86 LLM-drafted then hand-reviewed), 137 correct.
- A model failure is never counted as a blocked attack: if the classifier fails, the case goes to a human with the reason on the ticket, and is excluded from the scores.

**Limits:** small fixed sets, one free model, fictional data. Nothing here is evidence about other LLMs or real support traffic.

Stack: Python, FastAPI, bge-m3 retrieval, OpenRouter, MLflow. Written with Claude Code; the evaluation design and judgment calls are mine.

**Links**
- [GitHub repo](https://github.com/tses89214/stark-support-bot)
- [Full report (English)](https://tses89214.github.io/stark-support-bot/results/report.en.html) · [完整報告（中文）](https://tses89214.github.io/stark-support-bot/results/report.html)
