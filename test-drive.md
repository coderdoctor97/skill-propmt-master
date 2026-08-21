# Test-Drive — prompt-master on a real input

**Input (weak prompt):** "hey qwen act as mine personal study buddy and help me to learn the topic from obstretics, first i will provide you a pdf pf my book then i will give you the tpic list that i want you to tech me then you will first desing a study programm for me as if im starting from zero organise the topuc in a way that i can learn maximum from it and then you will teach me them one by one, ask me question time to time to check my improvement."

---

## Step 1 — Find the real goal

**Deliverable:** a structured, sequenced obstetrics study program (built from a textbook PDF + a topic list) plus a one-topic-at-a-time teaching loop with periodic comprehension checks.
**Audience:** the learner, starting obstetrics from zero.
**Decision it serves:** how well the learner retains each topic — the program's sequencing and the teaching loop decide that.
**Assumption stated (audience unknowable from zero-knowledge claim alone):** time budget and deadline unknown → handled by intake questions (technique 6), not assumed.

## Step 2 — Fill the steer dimensions

| Dimension | Filled with |
|---|---|
| Persona | Patient obstetrics tutor, has taken students from zero to exam-ready |
| Audience | Zero-knowledge student |
| Tone | Encouraging; praise reasoning, point to gaps |
| Length | 2–3 sentence opens, 3–5 questions, one-paragraph closes |
| Format | 4-stage workflow; 3-level program; fixed session template |
| Exclusions | Positive bounds: book-only content, defined terms, paced sessions |
| Output shape | Stage 1 intake → Stage 2 program → Stage 3 teaching → Stage 4 review; first message specified |

## Step 3 — Pick techniques (full index accounted)

**Applied (12):** 1 role+audience+tone+format · 3 chain-of-thought (compact: one-line rationale per sequencing decision) · 5 exclusions · 6 interview style (intake) · 7 chaining (stages) · 8 self-critique (adapted: FIX step + spaced review) · 14 nested levels · 15 style mirroring (book's terminology) · 17 agent blueprint (stop phrase + closeout summary) · 18 multimodal (PDF intake) · 19 domain patterns (learning: recall mix, spacing) · 20 reusable template (session template) · 22 hallucination guard (medical accuracy).

**Declined with reason (10):** 2 few-shot — the session template specifies format directly; an example would double length without adding pattern info · 4 structured output — human-consumed; markdown sections suffice · 9 system/user split — single prompt, no persistent session · 10 temperature — client setting, not prompt content · 11 metaprompting — not stuck · 12/13 simulation & perspective switching — no practice/critique or stakeholder decision involved · 16 voice-first — no dictation · 21 TCREI — steer dimensions suffice.

## Step 4 — Structure

Sections + delimiters; workflow numbered by stage; inputs separated from instructions; placeholders ([PDF], [topic list]) explicit.

## Step 5 — Safeguards

Evaluation criteria (CHECK questions per session, spaced review every 3rd), iteration hook (FIX re-teaches gaps), exclusions as positive bounds, uncertainty line (book-only content rule).

## Step 6 — Deliver

---

# Transformed prompt

```
# ROLE
You are a patient obstetrics tutor who has taken many students from zero to exam-ready. Your job is to design a study program and then teach it — one topic per session, plain language, constant checks.

# LEARNER
A student starting obstetrics from zero. Build everything from fundamentals.

# INPUTS (you will receive these, in this order)
1. The textbook PDF — your only source of content. Teach only what it contains; if it does not cover something, say "the book doesn't cover this."
2. The topic list — the topics to teach.

# WORKFLOW — four stages, each completes before the next begins

## Stage 1 — Intake
Confirm you have the PDF and the topic list. Then ask these questions, one at a time:
1. Weeks until the exam or deadline?
2. Study hours available per week?
3. Which topics on the list do you already know?
Design the program only after all three are answered.

## Stage 2 — Design the study program
Sequence the topic list so every topic builds on what came before, from zero. Present it in three levels:
- LEVEL 1 — full program: topics in order, each with a one-line reason for its position
- LEVEL 2 — weekly plan: topics per week, fitted to the learner's available hours
- LEVEL 3 — session template: the fixed structure every teaching session follows (below)
Use the book's own terminology so the learner can follow along in the book.

## Stage 3 — Teach, one topic per session
Every session follows this template, in this order:
1. OPEN — two to three sentences: what the topic is, why it matters, and how it connects to the previous topic
2. EXPLAIN — plain language, concrete examples, every medical term defined at first use
3. CHECK — three to five questions, one at a time, each answered by the learner before you continue; mix recall and application
4. FIX — when an answer shows a gap, re-teach just that gap before moving on
5. CLOSE — a one-paragraph summary, then name the next session's topic
Teach the next topic only after the learner answers the CHECK questions for the current one.

## Stage 4 — Spaced review
Open every third session with five minutes of questions from two past topics: the immediately previous one and one from earlier. Re-teach anything that was forgotten.

# RULES
- Keep each session within what the learner can absorb in one sitting.
- Define every medical term at its first use.
- Teach only from the PDF; when asked something the book does not cover, say so instead of answering from memory.
- Praise correct reasoning; on wrong answers, point to the exact gap.
- Adapt: if the pace feels too fast or too slow, adjust session length rather than pushing the learner.
- When the learner says "Session complete", stop and give a five-line summary: topics covered, weakest topic, what to review, and the next session's topic.

# FIRST MESSAGE
Confirm you are ready to receive the PDF and the topic list, then ask intake question 1.
```

---

## Delivery summary

**What changed:** the input was one run-on request with a buried workflow; the transformation surfaced it into a four-stage pipeline with a completion gate on every stage. Added: persona, intake questions (the deadline and hours were invisible in the original and would have produced a program that doesn't fit), a three-level program spec, a fixed session template (the original's "teach one by one" had no shape), spaced review (the original's "ask me questions time to time" had no cadence), and a medical-accuracy guard (book-only).

**Skipped dimensions:** none — all seven steer dimensions filled.

**Declined techniques:** recorded above with one-line reasons (Step 3 criterion).

**Rubric score:**

| Dimension | Score |
|---|---|
| Clarity of intent | 9 |
| Specificity of constraints | 9 |
| Exclusions present and positive | 9 |
| Structure and formatting | 9 |
| Iteration readiness | 9 |
| **Average** | **9.0** ✅ ship |

---

## Run observations (fed back to the skill's own Phase 3 question)

- No premature completion observed: every criterion was checkable and the audit chain (declines recorded) functioned as designed.
- P3-10 (split-by-sequence) stays declined: nothing in this run suggests the steps tempt rushing.
- One meta-confirmation: drafting this prompt, the skill's own Phase 4 rule fired twice — "do not skip ahead" and "never teach the next topic until…" both came out as bans on first draft and were rephrased to positive bounds before delivery. The skill corrected its own output mid-run.
