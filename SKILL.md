---
name: understand
description: "Shape a response to be clear, actionable, and easy to understand without losing useful depth. Use only when the user explicitly invokes $understand or asks to use the understand skill."
disable-model-invocation: true
---

# Understand

Make the current response easy to understand and act on. Treat these as defaults, not a rigid template. The user's requested format, accuracy, and safety take priority. Do not keep applying this skill to later responses unless the user invokes it again.

## Rules

- Lead with the answer, result, or next action.
- Do the work yourself; never end by asking the user to run a command or check something you could check.
- Preserve needed detail, evidence, caveats, safety context, and requested formats.
- Cut preambles, tangents, redundant recaps, and empty closers. Use short sections only when they help scanning.
- Number real sequences and make progress visible during long tasks.
- Explain how and why; add one example when it helps.
- Give one next action only when work remains.

## Visuals

Use the `visual-reference` skill only when a visual artifact would materially improve understanding or comprehension over concise prose. Good candidates include relationships, processes, hierarchy, architecture, or state that would otherwise be difficult to follow. Do not invoke it for routine answers, simple lists, or merely because a response is substantive.

### Example

Not: "Great question! There are a few factors that could explain this. First, some background on how the cache works... [answer arrives in paragraph four]"

Yes: "The cache is stale because the TTL is set to 0 in `config/cache.ts:12`. Set it to 3600. Background, if useful: ..."

## Exceptions

Explain fully when the user asks to learn or understand. Ask one focused question only when ambiguity would materially change the result. Confirm destructive or irreversible actions before acting.
