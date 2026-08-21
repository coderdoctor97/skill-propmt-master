---
name: prompt-master
description: Prompt mastery — use when the user's object is the prompt itself and they want it steered from weak to strong.
---

# Prompt Master

Turn a weak prompt into a strong one. **Prompting is programming in natural language.**

## The one move: steer

**Steer** = name every dimension the model could guess. The strong prompt is the one that leaves the least room to guess. Dimensions to steer:

- **Persona** — who the model embodies
- **Audience** — who reads the output
- **Tone** — the emotional register
- **Length** — a word or bullet budget
- **Format** — the shape of the output (sections, JSON, table)
- **Exclusions** — what must not appear
- **Output shape** — the visible end-state, so the model can tell when it is done

Specificity beats length: a tight 250-word prompt outperforms a rambling 1200-word one. The model has no memory beyond the window — repeat the key facts inside the prompt itself.

## The transformation process

Run the six steps in order. Start a step only when the previous one's criterion holds.

### Step 1 — Find the real goal

Look past the surface request to the deliverable behind it.

**Criterion:** You can state in one sentence the deliverable, its audience, and the decision or action it serves. If any of the three is unknowable from context, either interview the user (technique 6) or state the assumption in the delivered prompt.

Examples:

- "Help me with email." → a professional, non-salesy follow-up to a client about a 3-day project delay: new delivery date + next step.
- "Write a blog about AI." → a 1200-word practical guide for small e-commerce owners: three low-tech uses of AI in email marketing.

### Step 2 — Fill the steer dimensions (the 4Cs)

Fill every dimension in the list under "The one move: steer."

**Criterion:** Every dimension is filled, or declared not needed in the delivery summary.

### Step 3 — Pick techniques

Work the technique index (next section) in order.

**Criterion:** Every technique whose trigger matches is applied, or declined with a one-line reason recorded in the delivery summary.

### Step 4 — Structure the prompt

Write it like code: sections, delimiters, numbered steps; instructions separated from data; explicit output format.

**Criterion:** Instructions and data sit in separate, delimited blocks, and the output format is stated explicitly.

### Step 5 — Add safeguards and iteration hooks

- An evaluation criterion the model can check its own output against
- An iteration hook (technique 8)
- Exclusions as positive bounds (technique 5)
- On factual tasks, an uncertainty line (technique 22)

**Criterion:** The prompt carries an evaluation criterion, an iteration hook, exclusions as positive bounds, and — on factual tasks — an uncertainty line.

### Step 6 — Deliver

Output the transformed prompt, ready to copy or run.

**Criterion:** The delivery contains the transformed prompt, a summary of what changed (skipped dimensions and declined techniques included), and a rubric score (below). If the input already scores 8+ on the rubric, say so and return it lightly tightened.

## Technique index

All techniques, listed roughly by frequency of use. When applying a technique, open [`techniques.md`](techniques.md) at the matching number for its full treatment and examples.

1. **Role + audience + tone + format** — trigger: output feels generic or undirected. The highest-impact single change.
2. **Few-shot examples** — trigger: format, style, or pattern is hard to describe in words.
3. **Chain-of-thought** — trigger: logic, comparison, planning, pricing, or multi-step reasoning.
4. **Structured output** — trigger: output feeds another system.
5. **Exclusions** — trigger: a known unwanted pattern exists (greetings, jargon, salesy tone, apology).
6. **Interview style** — trigger: context is missing and the user is available.
7. **Prompt chaining** — trigger: task has stages where each output feeds the next.
8. **Self-critique** — trigger: the quality bar is high.
9. **System vs user prompts** — trigger: standing rules and identity must persist across a session.
10. **Temperature** — trigger: the task needs reliability (low) or variety (high).
11. **Metaprompting** — trigger: the prompt itself is stuck.
12. **Simulation & expert feedback agents** — trigger: the goal is practice or critique, not production output.
13. **Perspective switching** — trigger: a decision benefits from several stakeholder viewpoints.
14. **Nested complexity** — trigger: the deliverable has hierarchical levels.
15. **Style mirroring** — trigger: output must match a provided voice sample.
16. **Voice-first dictation** — trigger: the user dictates or runs the prompt by voice.
17. **Agent blueprint** — trigger: building a reusable specialized agent, not a one-shot prompt.
18. **Multimodal prompting** — trigger: input includes images, audio, or documents.
19. **Domain-specific patterns** — trigger: the task sits in content, code, strategy, or learning.
20. **Reusable templates** — trigger: the task recurs.
21. **TCREI frame** — trigger: a named methodology is wanted (Google's Task-Context-References-Evaluate-Iterate).
22. **Bias & hallucination safeguards** — trigger: the task is factual and consequential.

## Rubric

Score the transformed prompt 1–10 on each dimension. Ship at an 8+ average; below that, strengthen the weak dimension and rescore.

- Clarity of intent
- Specificity of constraints
- Exclusions present and positive
- Structure and formatting
- Iteration readiness

## Failure modes

When a transformed prompt still misses, fix by row. Debug in this order: persona → constraints → examples → split into chains → exclusions → self-critique.

| Symptom | Fix |
|---|---|
| Generic or irrelevant output | → technique 1 |
| Incomplete or mixed results | → technique 7 |
| Wrong format or style | → technique 2 |
| Wrong length, tone, structure | → steer the Length, Tone, Format dimensions |
| Forgotten details | → the no-memory rule (steer) |
| Wall of text | → technique 4 |
| Mediocre first output | → technique 8 |
| Unwanted elements | → technique 5 |
| Hallucinated facts | → technique 22 |
| Missing nuance | → technique 6 |

## Golden rule

**Steer** every dimension you can name.

---

Sources: Google's prompt-engineering course and expert masterclasses.
