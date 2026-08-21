# Techniques — full reference

Reached from [`SKILL.md`](SKILL.md) when applying a technique. Numbers match the technique index in `SKILL.md`; each entry gives the trigger, how to write it, and examples.

## 1. Role + audience + tone + format

**Trigger:** output feels generic or undirected.

The highest-impact single change. A clear persona, reader, register, length, and structure shrink the model's guessing space.

Weak: "Write something about our product."

Strong: "You are a senior B2B copywriter with eight years of experience helping SaaS companies create high-converting LinkedIn content. Write a two-sentence LinkedIn ad for our project management tool that is a simpler, more visual alternative to Asana. Target audience: operations managers at midsize companies (50–200 employees) who are frustrated with overly complex tools. Tone: confident but not salesy. End with a clear, soft CTA. Keep the entire ad under 140 characters."

Also: "You are a patient kindergarten teacher. Explain how photosynthesis works to a frustrated 6-year-old using simple analogies and encouraging language."

## 2. Few-shot examples

**Trigger:** format, style, or pattern is hard to describe in words.

Give 2–3 input→output pairs so the model infers the exact pattern, tone, and format.

```
Turn user feedback into a short support ticket title (maximum 60 characters)
using this exact format: [Area] - Brief description

Example 1:
Feedback: Login is broken with Google and Safari
Title: Google Login - Fails on Safari

Example 2:
Feedback: Export to CSV only exports first 100 rows
Title: CSV Export - Only first 100 rows

Now process this new feedback:
Feedback: The app crashed when I uploaded a PDF over 10MB on iPhone
```

## 3. Chain-of-thought

**Trigger:** logic, comparison, planning, pricing, or multi-step reasoning.

Force the model to show its reasoning before the final answer. Cuts errors on multi-step problems.

"Think step by step. Show your complete reasoning process before giving the final answer. Consider user psychology, revenue sustainability, competitor pricing, and implementation difficulty."

## 4. Structured output

**Trigger:** output feeds another system.

Request a machine-readable format — and the schema alone in response.

"Return only valid JSON with this exact schema. Do not include any other text or explanation:

{
  \"competitor_name\": \"\",
  \"pricing_model\": \"\",
  \"key_features\": [],
  \"limitations\": [],
  \"strategic_recommendation\": \"\"
}"

## 5. Exclusions

**Trigger:** a known unwanted pattern exists (greetings, jargon, salesy tone, apology).

Negative constraints suppress unwanted patterns the model has seen in training. Phrase them as positive bounds where possible; when a ban is needed, pair it with the positive target.

- Keep the entire response under 150 words
- Open with the answer, not a greeting
- Use simple analogies suitable for a 15-year-old
- Plain language, one flowing paragraph
- State the limit directly rather than apologizing for it
- Concrete claims only — no hype words or superlatives

## 6. Interview style

**Trigger:** context is missing and the user is available.

Let the model ask for what it needs before producing output.

"I need a 250-word LinkedIn post about lessons learned after switching to a 4-day work week. Before you write anything, interview me one question at a time. When you have enough information, say exactly: 'I have enough information' and then write the post."

## 7. Prompt chaining

**Trigger:** task has stages where each output feeds the next.

Break complex projects into sequential steps.

1. Generate 10 podcast name ideas targeting indie game developers with a playful tone
2. Write compelling 2-sentence taglines for the top 3 names explaining why listeners should care
3. Create a complete 4-week launch plan using the winning name and tagline

Four chaining patterns: **sequential** (output of one → input of next), **parallel** (independent prompts run side by side), **recursive** (model critiques and rewrites its own output), **conditional** (path chosen by an intermediate result).

## 8. Self-critique

**Trigger:** the quality bar is high.

After the first output, have the model evaluate and improve it. Refinement phrases to keep on hand:

- "Make this more concise while keeping all key points"
- "Add more specific examples"
- "Adjust the tone to be more [X]"
- "Expand the weakest section"
- "Rewrite for a more expert audience"

Rating prompt: "Rate the above response from 1 to 5 on clarity and completeness. In one sentence, suggest the single most important improvement. Then apply that improvement to create a revised version."

## 9. System vs user prompts

**Trigger:** standing rules and identity must persist across a session.

System prompts carry persistent identity, rules, and style; user prompts carry the specific task.

System: "You are a helpful coding assistant who always explains concepts simply, provides working code examples, and defines jargon before using it."

## 10. Temperature

**Trigger:** the task needs reliability or variety.

- **Low (0.1–0.3):** factual, consistent, structured — code, data analysis, legal summaries, technical writing, reports
- **High (0.7–1.0):** creative, varied — brainstorming, storytelling, marketing copy, ideation

## 11. Metaprompting

**Trigger:** the prompt itself is stuck.

Have the model improve its own prompt.

- "How can I make this prompt more specific and effective?"
- "What important context am I missing for better output?"
- "Rewrite this prompt using the 4C framework with stronger constraints and clearer structure."

## 12. Simulation & expert feedback agents

**Trigger:** the goal is practice or critique, not production output.

Create specialized agents for practice and critique.

Simulation: "Act as a skeptical senior hiring manager with 12 years of experience. Interview me for a Project Manager role using behavioral questions one at a time. Continue until I say 'End session', then provide detailed feedback and specific improvement suggestions."

Feedback: "You are a world-class sales copywriter with 15 years of experience. Critique this cold email for subject line effectiveness, value clarity, and call-to-action strength. Be brutally honest and then provide a rewritten version."

## 13. Perspective switching

**Trigger:** a decision benefits from several stakeholder viewpoints.

Examine an issue from multiple viewpoints, then synthesize.

"Analyze this business decision from three perspectives: (1) as a conservative CFO focused on financial risk, (2) as an aggressive growth strategist focused on market opportunity, and (3) as a cautious operations manager focused on execution challenges. Then synthesize the insights into actionable recommendations."

## 14. Nested complexity

**Trigger:** the deliverable has hierarchical levels.

Structure large deliverables in explicit levels.

"Create a content marketing strategy with three nested levels:
Level 1: Overall strategy and goals
Level 2: Monthly themes and content pillars
Level 3: Specific content pieces for month one including titles, target audience, key points, and distribution channels for each piece."

## 15. Style mirroring

**Trigger:** output must match a provided voice sample.

Provide writing samples so the model matches the exact voice.

"Analyze the writing style, sentence structure, tone, and communication approach in the three emails I provided. Now write a follow-up email to the same client about project delays while matching my exact communication style."

## 16. Voice-first dictation

**Trigger:** the user dictates or runs the prompt by voice.

Dictating captures richer nuance faster than typing. When using voice mode:

- Speak naturally; include every detail as it comes to mind
- Use clear transitional phrases ("First…", "Next…", "Finally…")
- Ask the model to ask clarifying questions
- Structure voice prompts with explicit sections for role, context, constraints, and command
- Have the model summarize what it understood before proceeding

## 17. Agent blueprint

**Trigger:** building a reusable specialized agent, not a one-shot prompt.

1. Assign a clear, specific persona
2. Inject relevant business or domain context
3. Define the exact interaction pattern
4. Set a stop phrase ("Session complete")
5. Instruct the agent to summarize top recommendations when the stop phrase is used

## 18. Multimodal prompting

**Trigger:** input includes images, audio, or documents.

- Upload screenshots and ask for strategic UX or marketing analysis
- Upload competitor pricing pages and request competitive intelligence
- Upload audio and ask the model to describe mood and suggest arrangement changes

## 19. Domain-specific patterns

**Trigger:** the task sits in content, code, strategy, or learning.

| Domain | Patterns to include |
|---|---|
| Content creation | Audience pain points, desired emotional response, hooks, structure, CTAs, tone and length constraints |
| Code & technical | Language, framework, constraints, testing requirements, explanations alongside code, edge cases |
| Business strategy | Perspective switching, actionable frameworks with timelines, success metrics |
| Learning & education | Feynman technique (explain simply, then identify gaps), personalized paths with assessment, spaced repetition |

## 20. Reusable templates

**Trigger:** the task recurs.

Build master templates for recurring tasks — client onboarding, content briefs, cold outreach, meeting summaries, performance reviews — with clearly marked variables. Keep them versioned in a categorized library (marketing, engineering, HR, sales) and refine the best performers over time.

## 21. TCREI frame

**Trigger:** a named methodology is wanted.

Google's alternate lens to the steer dimensions:

- **Task** — precise description of the desired output
- **Context** — all necessary background
- **References** — examples of desired style or format
- **Evaluate** — systematic checking against criteria
- **Iterate** — refinement loop based on evaluation

## 22. Bias & hallucination safeguards

**Trigger:** the task is factual and consequential.

Build verification into the prompt:

- "Only use information from the provided text. If unsure, say 'I don't have enough information.'"
- Request citations where possible
- Instruct the model to flag uncertainty explicitly
- Keep a human in the loop for anything consequential
