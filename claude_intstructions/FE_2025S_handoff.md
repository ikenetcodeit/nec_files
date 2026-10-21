# Handoff: FE exam prep, 2025S mock review (as of Wed Oct 21, 2026)

## Who the user is and how to work with them
- CS student and practicing app developer (TS/React/Next.js, React Native, Java/Spring Boot, Kotlin, C#/.NET, SQL, Docker). Preparing for the **ITPEC FE exam**, assumed **Sun Oct 25, 2026** (Subject A 9:30–11:00, Subject B 12:30–14:10; user should confirm on their admission card).
- Wants a **senior engineer / mentor** voice: direct, no yes-manning, explain reasoning and trade-offs, connect exam topics to real engineering practice, and occasionally ask them to reason before revealing an answer (one question at a time). Don't over-lecture when they need something done fast.
- Project files: `claude_FE_Study_Plan_Oct2026.md` (16-day sprint plan, error-log rules, domain→question-range map), FE Exam Preparation Book Vol.1 and Vol.2 (Vol.1 = Subject A theory; Vol.2 mostly old-format, only Ch6–7 useful for Subject B).

## What was built
**`fe_2025S_answer_checker.html`** (single-file HTML; the user must re-upload it if the new agent needs to edit it).
- Two papers (2025S Subject A: 60 Qs, choices a–d; Subject B: 20 Qs, choices a–j because the key includes "i").
- Flow: mark answers on a bubble sheet (click or keyboard; `?` flags a guess) → **Check my answers** → results with score, per-domain table against a 60% line, filterable question list, a "Why" dropdown per miss, and **Copy error log** (TSV for a spreadsheet).
- Official keys are embedded as constants and are the single source of truth; saved state (`window.storage`, key `fe-checker:2025S`) restores answers/guesses/reasons but never the key.
- Domain ranges used: A = Q1–7 CS fundamentals, 8–17 systems, 18–22 DB, 23–26 network, 27–33 security, 34–40 development, 41–45 management, 46–60 strategy. B = Q1–7 control flow, 8–11 data structures/sorting, 12–16 strings/applied, 17–20 security.

**Known issue to fix (offered, not yet done):** the "Lucky guess" reason label is ambiguous. The user applied it to *wrong* answers and never used the guess flag. Rename it to "Guessed" and have selecting it set the guess flag automatically.

**Lesson already taught:** the first hand-typed key strings were wrong (59 and 19 chars, answers shifted). Caught by a script and rebuilt from the PDF tables with a per-question check. Point: validate hand-transcribed data item by item, not just by length.

## Official answer keys (verified against ITPEC PDFs, 39th FE exam, April 2025)
- **Subject A (Q1→Q60):** `aabcddacccccdaccccbdacabccabbdbbcbccdbdbaabdcdccadbdbbcabbdb`
- **Subject B (Q1→Q20):** `fdbgahbfceghcffceeig`

## Results
**Subject A: 29/60 (48%), below the 60% line.**

| Domain | Score |
|---|---|
| CS fundamentals | 3/7 |
| Computer systems | 5/10 |
| Database | 3/5 |
| Network | **1/4** (weakest) |
| Security | 4/7 |
| Development | **2/7** |
| Management | 3/5 |
| Strategy | 8/15 (most points lost) |

Missed: 1, 4, 6, 7, 11, 12, 14, 15, 17, 19, 21, 24, 25, 26, 27, 28, 30, 34, 35, 37, 39, 40, 41, 42, 46, 47, 50, 53, 55, 56, 59.
Reasons: 18 didn't know, 9 guessed (mislabeled "Lucky guess"), 3 misread (Q19, Q27, Q37), 1 "ran out of time" (Q1, which is suspicious for the first and easiest question; asked the user, no answer yet).

**Subject B: 12/20 (60%), raw estimate only (the real exam weights by difficulty).**
Missed: Q4 (guess), Q7 (calc slip), Q11 (time), Q14 (guess), Q15 (calc slip), Q16 (calc slip), Q18 (didn't know), Q19 (didn't know). Q8–10 data structures all correct.

## Diagnosis given to the user
- Subject A is the bottleneck, and it's a **vocabulary/knowledge gap, not technique** (27 of 31 misses). Many misses are concepts they use as a developer, just under exam names: Q28 least privilege, Q24–26 network layer/ARP/ping→traceroute, Q34 microservices, Q39 reverse engineering, Q40 Sprint.
- Calculation misses (Q12 availability 0.99−0.81=0.18, Q14 preemptive priority scheduling, Q15 1024×768×3 B×10 ns ≈ 24 ms) are on the plan's "repeated calculations" list; redo by hand.
- Subject B misses are mostly **tracing slips**, so the fix is a written variable table for every question.
- Because the guess flag wasn't used, true Subject A knowledge may be below 48%.

## Adjusted plan for the remaining days
- **Wed Oct 21:** per the plan's "A < 50%" rule, ~45 min strategy flashcards (2025S Q46, 47, 53, 55, 56, 59, then 2024S/A strategy questions) plus ~45 min Network and Development (Vol.1 Ch4 vocabulary; Q23–26 and Q34–40 from 2025A and 2026S).
- **Thu Oct 22:** as planned (B Q12–16 from 2024A/2025A; B Q17–20 from 2025S/2025A), with a variable table on every trace.
- **Fri Oct 23:** 2024A Subject A timed mock. Use the guess flag properly to get a real knowledge baseline.
- **Sat Oct 24:** review only (2024S Subject B timed, then error log and flashcards). No new topics.

## Open threads
1. Pending challenge to the user: explain why sending the PIN through a separate channel is correct for Q30, and what attack mailing it with the card enables.
2. Ask what happened with Q1 ("ran out of time").
3. Offer to fix the "Lucky guess" label in the checker, or to extend the checker to other papers (2025A, 2024A, etc.) once the user provides those keys.
