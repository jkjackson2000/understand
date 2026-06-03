---
name: understand
description: "Teach, explain, or reshape an answer so the user genuinely comprehends and can use it — leading with the governing idea, showing the mechanism, using worked examples, and checking understanding rather than just simplifying. Use when the user invokes $understand, says they don't follow, asks to learn or understand something, wants an explanation adapted to their level, or asks for an answer optimized for comprehension rather than simplification."
---

# Understand

Help the user comprehend the thing they asked about well enough to act, explain it back, or make a decision.

This skill is not a "make it shorter" pass. Use brevity when it reduces cognitive load, but keep or add detail when it improves comprehension, accuracy, transfer, or retention.

This is a comprehension workflow, not a tool restriction. Use normal tools, code edits, searches, docs, and verification whenever they improve the answer.

## Operating Modes

### Teach or Explain

Use when the user asks to understand, learn, reason through, debug conceptually, compare options, or make sense of unfamiliar material.

1. Identify the learning target: what the user needs to understand, decide, do, or explain back.
2. Infer the user's current model from their wording, errors, examples, and level of specificity.
3. If the target, audience, or missing context changes the right explanation, ask one focused clarifying question before answering.
4. If enough context exists, answer directly and state any assumption that matters.
5. Use research-supported techniques from the comprehension pass below; choose the smallest set that makes the material understandable.

### Reshape an Existing Answer

Use when the user gives text or refers to a prior answer and asks for `$understand`, clearer explanation, better teaching, or stronger comprehension.

1. Select the target:
   - If the user supplied text, transform that text.
   - If the user named a span, transform only that span.
   - If no target is supplied, transform the most recent substantive assistant message in the conversation.
2. Preserve the source facts unless the user explicitly asks you to correct or expand them.
3. You may add structure, examples, checks for understanding, or missing connective tissue when they are implied by the source and improve comprehension.
4. If a factual gap blocks comprehension, ask for the missing information or say what would need to be verified.

### Research or Document

Use when the answer depends on domain facts, code behavior, docs, standards, or scientific claims.

1. Prefer primary sources: project files, official docs, specifications, papers, logs, tests, or measurements.
2. Separate verified facts from inference.
3. Avoid "scientifically proven" overclaiming. Say "research-supported" or "evidence-informed" unless citing a specific result.
4. When sources conflict, explain the conflict and use the most relevant, recent, and directly observed evidence.

## Comprehension Pass

Apply these checks in order. The goal is comprehension, not maximum compression.

1. **Start from the user's purpose.**
   State what they are trying to understand or decide, then aim every paragraph at that purpose. If purpose is unclear and changes the answer, ask first.

2. **Lead with the governing idea.**
   Sentence 1 should give the central answer, mental model, decision, correction, or root cause. If the reader stops after sentence 1, they should still know what matters.

3. **Build from known to new.**
   Anchor the explanation in something the user already understands, then add one new distinction at a time. Define terms at first use only when the user has not already shown they know them.

4. **Chunk for working memory.**
   Use one idea per paragraph. For 5+ parallel items, group them under 2-4 content-bearing labels. Put related facts next to each other so the user does not have to integrate scattered pieces.

5. **Make the mechanism visible.**
   For concepts, bugs, decisions, and workflows, show the causal chain: what happens, why it happens, what follows from it, and what changes when one part changes.

6. **Use examples before abstraction when the user is learning.**
   For a hard or unfamiliar idea, show one concrete worked example with real values or a realistic scenario, then name the general rule. For experts, give the rule first and keep examples optional.

7. **Prompt active processing.**
   When comprehension matters more than speed, include a quick self-check, prediction question, or "you know you understand it when..." criterion. Do not quiz the user when they only need a direct answer.

8. **Calibrate confidence and evidence.**
   Assert plainly when evidence is strong. Hedge only when uncertainty is real and decision-relevant. Separate verified facts from inferences. Never invent precise numbers, versions, dates, citations, or probabilities.

9. **Remove load that does not teach.**
   Delete praise, restated questions, throat-clearing, self-narration, vague previews, reflexive hedges, redundant prose, and jargon that hides fuzzy thinking. Keep length only when it earns comprehension.

10. **Correct the learner's model, not their feelings.**
   If the user's premise is wrong, say so clearly and explain from evidence. Do not validate an incorrect model just to be agreeable.

## Gated Additions

Add these only when they improve comprehension.

- Clarifying question: ask when audience, goal, context, constraints, or source facts would materially change the explanation.
- Worked example: use for difficult or unfamiliar ideas. Show the concrete case before the abstract rule for non-experts.
- Analogy: use for unfamiliar concepts when it maps relationships clearly. Name where the analogy breaks.
- Diagram in words: use when spatial, layered, or process structure matters and no visual is available.
- Table: use only when multiple items share the same attributes.
- Self-check: use when the user is learning a concept, not just consuming an answer.
- One-clause why: use after a non-obvious step or setting so the user can reason from the rule later.

## Output Shape

Use this as a scaffold, not a form:

```text
<Governing idea or direct answer.>

<Plain-language mental model, grounded in the user's context.>

<Mechanism or causal chain: what happens, why, and what follows.>

<Worked example, analogy, comparison, or steps only if it helps comprehension.>

<Check for understanding or next action, when useful.>

<Caveats or uncertainty, only if decision-relevant.>
```

Avoid headings for short answers. For longer answers, use headings that carry meaning, not generic labels like "Overview", "Notes", or "Details".

## Anti-Patterns

Remove these whenever possible:

- Treating comprehension as simplification, summarization, or token compression.
- Answering before asking a needed clarifying question.
- Definition-first explanations that never show how the idea works.
- Abstract rules with no example when the user is a novice.
- Examples that skip the exact steps the learner has not automated.
- Walls of text, flat lists longer than working memory can hold, and bullet soup that fragments cause-and-effect reasoning.
- Prose that reads code, commands, or tables aloud instead of explaining why they matter.
- Generic headings.
- Reflexive over-hedging, false precision, or unsupported scientific certainty.
- Sycophantic validation and false balance.
- Jargon that hides fuzzy thinking, or definitions the reader clearly does not need.
- Length used as a substitute for teaching.

## Reference

Read `references/technique-reference.md` when you need the research basis, examples, or a close judgment call. The instructions above are enough for normal use.
