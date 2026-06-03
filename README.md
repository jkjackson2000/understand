# understand

**Stop getting answers you can't actually use.** `understand` is a skill for Claude Code and Codex that optimizes the model's answers for *your comprehension* — not brevity, not token count, not a tidy summary.

LLMs already produce correct, dense, comprehensive answers faster than you can absorb them. The bottleneck isn't the answer — it's understanding it well enough to act on it, decide, or explain it back to someone else. So instead of compressing, `understand` makes the answer land: it leads with the governing idea, shows the mechanism, uses a worked example when you're learning, and checks that it stuck.

It is **not** a "make it shorter" pass. It cuts the words that don't teach and keeps — or adds — the ones that do.

---

## See the difference

**Prompt:** *"What's a database index and why would I add one?"*

<table>
<tr><th>Default answer</th><th>With <code>understand</code></th></tr>
<tr><td valign="top">

> A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space to maintain the index data structure. Indexes are used to quickly locate data without having to search every row in a database table every time a database table is accessed. There are several types of indexes including B-tree, hash, and...

</td><td valign="top">

> **Add an index when a query has to scan the whole table to find a few rows.** An index is a sorted lookup that lets the database jump straight to those rows instead.
>
> Mechanism: without an index, `WHERE email = ...` reads every row to find matches — that's why it slows down as the table grows. An index keeps `email` values pre-sorted with pointers to their rows, so the database binary-searches to the match. Scan → lookup.
>
> Analogy: it's the back-of-book index. Without it you read every page; with it you jump to the right ones. Limit: each index costs storage and makes writes slightly slower, because every insert must update the index too.
>
> You've got it when you can predict that an index on `email` speeds up `WHERE email = ...` but does nothing for `WHERE country = ...`.

</td></tr>
</table>

Same facts. The right-hand version leads with the decision, shows the causal chain, maps an analogy and names where it breaks, and ends with a check you can use to test yourself — so the idea is *yours* to apply, not just to nod at.

---

## What it does

When the skill is active, it pushes the assistant through three moves:

**Diagnose** — work out whether you need a decision, a concept, a procedure, a debugging model, or a correction, and ask one focused question when the answer would genuinely change.

**Explain** — lead with the governing idea (sentence one is the answer, not throat-clearing), build from what you already know to what's new, make the mechanism visible (*what happens, why, and what follows*), and show a worked example before the abstraction when the material is unfamiliar.

**Verify** — give you a way to check the idea landed, and calibrate confidence: assert plainly where evidence is strong, hedge only where uncertainty is real, and never invent numbers or citations.

Each move is grounded in a named body of research — cognitive-load theory, the worked-example effect, retrieval practice, split-attention, dual coding, and more. The evidence layer lives in [`references/technique-reference.md`](./references/technique-reference.md).

---

## Install

The repository **is** the skill (`SKILL.md` lives at the root), so the simplest install is to clone it straight into your agent's skills directory — `~/.claude/skills/` for Claude Code, `~/.codex/skills/` for Codex:

```bash
git clone https://github.com/jkjackson2000/understand.git ~/.claude/skills/understand
# Codex: same command, but clone into ~/.codex/skills/understand instead
```

**Prefer one checkout you can `git pull` to update everywhere?** Clone once and symlink it in:
```bash
git clone https://github.com/jkjackson2000/understand.git ~/projects/understand
ln -s ~/projects/understand ~/.claude/skills/understand   # and/or ~/.codex/skills/understand
```

**Update:** `cd ~/.claude/skills/understand && git pull`

---

## Using it

The skill is discoverable automatically — Claude reaches for it when you ask to learn, understand, or get an answer pitched at your level. You can also invoke it explicitly:

- `$understand` — apply the comprehension workflow to your next request.
- *"I don't follow — can you `$understand` this?"* — reshape the previous answer so it lands.
- *"Explain X so I actually get it"* — diagnose your level and teach from there.

It has three modes: **Teach or Explain** (new material), **Reshape an Existing Answer** (take a prior answer and make it comprehensible), and **Research or Document** (ground the answer in primary sources). The full workflow is in [`SKILL.md`](./SKILL.md).

---

## Why this exists

The idea comes from Andrej Karpathy's recurring point that as AI agents take over execution, the human becomes the bottleneck — and what bottlenecks us isn't producing the work, it's understanding it well enough to direct, judge, and trust it. A model that hands you a correct answer you don't actually grasp hasn't removed the bottleneck; it's just moved it somewhere harder to see. This skill is a deliberate attempt to attack that gap.

(The README you're reading was itself written using the skill — which is the most honest test I can offer of whether it works.)

---

## How it's organized

| File | Purpose |
|---|---|
| [`SKILL.md`](./SKILL.md) | The skill itself — operating modes, the comprehension pass, gated additions, anti-patterns. Enough to run on its own. |
| [`references/technique-reference.md`](./references/technique-reference.md) | The evidence layer: each technique with its rule, the cognitive principle behind it, a before→after, and the research anchors. |
| [`agents/openai.yaml`](./agents/openai.yaml) | Codex UI metadata (display name, prompt). |

This follows the progressive-disclosure pattern Anthropic recommends for skills: a lean `SKILL.md` that loads on every use, with the heavy reference material pulled in only when a judgment call needs it.

---

## The evidence behind it

The skill is **evidence-informed, not magic.** It draws on cognitive-load theory (Sweller), working-memory chunking (Cowan), the worked-example effect (Renkl, Atkinson), self-explanation and elaborative interrogation (Chi, Pressley, Dunlosky), retrieval practice (Roediger & Karpicke), multimedia learning and signaling (Mayer), and structure-mapping analogy (Gentner). Most findings are robust at the principle level but context-sensitive in application — which is why the skill says "research-supported," not "scientifically proven." Full anchors are in the [technique reference](./references/technique-reference.md#research-anchors).

---

## Contributing

Issues and pull requests are welcome — see [CONTRIBUTING.md](./CONTRIBUTING.md). The single most useful contribution is a real failure case: a prompt, the answer the skill produced, and what would have helped you understand it better.

## License

[MIT](./LICENSE) © 2026 Jared Jackson. Free to use, modify, and redistribute — just keep the copyright notice.

If this skill helps you, a ⭐ on the repo is appreciated and helps others find it.
