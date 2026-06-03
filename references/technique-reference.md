# understand — technique reference

The evidence layer behind `SKILL.md`. Each technique gives the **rule**, the **why** (the cognitive or learning principle), and a **before → after**. Read this when a rule needs justification or a judgment call is close; `SKILL.md` alone is enough to execute.

This skill is evidence-informed, not magic. It draws from cognitive-load theory, worked-example research, self-explanation and elaborative interrogation, retrieval practice, formative assessment, dual coding / multimedia learning, information design, technical communication, and agent-specific failure modes. Most findings are robust at the principle level but context-sensitive in application, so prefer "research-supported" over "scientifically proven" unless citing a specific study or measurement.

---

## Core Goal

The user should leave with a usable mental model, not just a shorter answer. A usable mental model lets them:

1. Recognize the idea in a new situation.
2. Predict what happens when a condition changes.
3. Explain the idea back in their own words.
4. Take the next correct action without memorizing isolated steps.

---

## Tier 1 — Comprehension Core

### 1. Diagnose the learner's goal
**Rule.** Identify whether the user needs a decision, a concept, a procedure, a debugging model, a comparison, or a correction. If the target or audience would change the answer, ask one focused clarifying question before explaining.
**Why.** Effective instruction starts from prior knowledge and task goal. Without that, the answer may be accurate but aimed at the wrong cognitive job.
**Example.** Before: "Caching stores data for later." → After: "Are you trying to understand caching conceptually, or decide where to add it in this app? Those need different explanations."

### 2. Lead with the governing idea
**Rule.** Make sentence 1 the central answer, mental model, decision, or correction. For yes/no questions, the first word resolves it. Test: if the reader stopped after sentence 1, would they know what matters?
**Why.** Attention and working memory are highest at the top. The governing idea becomes the schema later details attach to, which lowers integration cost.
**Example.** Before: "There are several factors to weigh, and it depends on your setup..." → After: "Use a connection pool: your code opens a socket per request, so connection setup is the bottleneck."

### 3. Build from known to new
**Rule.** Anchor the new idea in something already present in the prompt, then add one new distinction at a time. Define terms at first use only when the user has not shown they know them.
**Why.** New information is easier to encode when it connects to prior schemas; over-explaining familiar material wastes attention and makes experts skim past the useful part.
**Example.** Novice: "A promise is a placeholder for a value that will arrive later." Expert: "This promise chain loses the rejection because the inner promise is not returned."

### 4. Chunk into short paragraphs and capped lists
**Rule.** One idea per paragraph. Count parallel items before emitting a list; if 5+, partition into 2-4 labeled groups so no level has more than ~4 siblings. Put explanation next to the code, term, command, or decision it explains.
**Why.** Working memory holds only ~4 independent chunks (Cowan); a wall of text or a flat 8-item list overflows the buffer and never coheres into one understood whole. Whitespace and grouping are the delimiters that define a chunk.
**Example.** Before: flat 8-bullet CLI-flag list. After: "Input flags (3) / Output flags (2) / Debug flags (3)" — three chunks.

---

## Tier 2 — Teaching Moves

### 5. Worked example before the rule for novices
**Rule.** For hard or unfamiliar material, show one complete concrete instance with real values or a realistic scenario, then name the abstract rule. For experts, give the rule first and make the example optional.
**Why.** The worked-example effect: novices learn faster from a complete trace than from a bare rule that forces them to juggle goal, rule, and step search at once. Expertise reversal means the same detail can slow an expert.
**Example.** Before: "To debug a race, add synchronization." → After: "A reads counter=5, B also reads 5, both write 6, so one increment is lost. The general rule: any read-modify-write on shared state needs synchronization."

### 6. Make the causal chain explicit
**Rule.** Explain mechanism as situation → action/event → consequence → fix or implication. Use "because", "so", and "which caused" instead of disconnected "also/next/additionally".
**Why.** Causal structure supports prediction and transfer. The user can reuse the model when surface details change.
**Example.** Before: "Endpoint slow. Query lacked index. Added index." → After: "The page was slow because the query scanned every order for each customer. Adding an index turned the scan into a lookup, so latency dropped."

### 7. Co-locate what must be understood together
**Rule.** Place each explanation immediately adjacent to its target. Annotate a code line with an inline comment on that line, not a paragraph 10 lines later. Define a term at first use, not in a glossary. Eliminate "see above/below" — if B is needed to understand A, move B next to A. If two facts must be combined to act, put them in one sentence.
**Why.** The split-attention effect: separating sources that must be integrated burns working memory on navigation and re-finding instead of comprehension.
**Example.** Before: "Set the timeout (see config note at end)." …50 lines later… "Note: timeout is in ms." → After: "Set timeout to 5000 (milliseconds)."

### 8. Use analogy only when it maps structure
**Rule.** Use one analogy for an unfamiliar concept only when the relationships match. State the mapping and the limit.
**Why.** Structure mapping lets the learner import an existing schema; weak analogies transfer the wrong properties.
**Example.** "A DB index is like a book's back-of-book index: without it you scan every page; with it you jump to likely pages. Limit: database indexes cost storage and make writes slightly slower."

### 9. Ask the learner to retrieve or predict
**Rule.** When teaching rather than merely answering, add a small check: "You know you have it when...", "Predict what happens if...", or "Try explaining it as...".
**Why.** Retrieval practice and generation improve durable learning more than rereading. A check also reveals whether the explanation landed.
**Example.** "You understand this if you can predict which query uses the index before running `EXPLAIN`."

### 10. Explain the why behind non-obvious steps
**Rule.** Add a one-clause rationale for settings, steps, and recommendations that would otherwise be memorized.
**Why.** Self-explanation and elaborative interrogation deepen retention by connecting a rule to a reason.
**Example.** Before: "Use exponential backoff." → After: "Use exponential backoff so retries spread out instead of piling more load onto an already failing service."

---

## Tier 3 — Communication Controls

### 11. Use one channel per fact
**Rule.** After drafting, scan for any sentence that restates what an adjacent code block, command, table, or formula already states exactly. Delete it. Reserve prose beside code for what the code does not say: why, caveat, consequence, or interpretation.
**Why.** The redundancy effect: identical content in two streams forces reconciliation rather than reinforcing understanding.
**Example.** Before: a `git reset --hard origin/main` block then "This runs git reset hard to origin main." → After: the block, then only "Discards uncommitted work — irreversible."

### 12. Tables only for shared attributes
**Rule.** If content has the shape "N items each described on the same M attributes" (options vs criteria, before/after, version diffs, tradeoffs), render a table with items as rows, attributes as columns, short phrases per cell. Do NOT table one-dimensional, narrative, or single-comparison data — use a sentence.
**Why.** Prose hides structure and forces the reader to rebuild the grid in working memory; a table cuts comprehension time (~43%) at equal accuracy for material that requires comparison.
**Example.** Before: "Redis is in-memory, fast, volatile; Postgres is disk-based, durable, slower for KV…" → After: a 2-row table, columns Storage | Speed | Durability.

### 13. Content-bearing headings on long replies
**Rule.** Add headings when a reply exceeds ~4 sentences or covers 3+ subtopics. Make every heading a cue the reader can use while scanning ("Why the build fails", not "Background").
**Why.** Signaling offloads the work of finding what matters onto the page; generic labels carry no information.
**Example.** Before: "## Notes". After: "## The bug: stale token cached after refresh".

### 14. Lists only for true parallel sets
**Rule.** Bullet only 3+ sibling items of the same kind. Number when order or count matters; bullet when it does not. Keep cause-effect, tradeoff reasoning, and narrative in prose.
**Why.** Lists chunk parallel members for scanning, but fragmenting an argument into equal-weight bullets removes the logic between steps.
**Example.** Reasoning stays prose: "This fails under load because connections are not reused." Three alternative fixes can become three bullets.

### 15. Delete non-teaching words
**Rule.** Cut praise, restated questions, throat-clearing, self-narration, vague previews, reflexive hedges, and definitions the asker clearly does not need.
**Why.** Extraneous cognitive load competes with the material the learner is trying to encode.
**Example.** Before: "That's a really interesting question! Basically, I think you want a lock." → After: "Use a lock."

### 16. State confidence once, calibrated
**Rule.** Assert plainly. Hedge only where uncertainty is real and decision-relevant. Separate what you verified from what you inferred. Never invent precise numbers, versions, dates, citations, or probabilities.
**Why.** Blanket hedging lets conjecture impersonate fact; calibrated uncertainty helps the user know what they can rely on.
**Example.** Before: "This might possibly help in some cases." → After: "This fixes the bug on Postgres 14+. I have not checked older versions; verify that the flag exists there."

### 17. Bold sparingly; monospace for identifiers
**Rule.** Bold at most ~one load-bearing term per paragraph — the noun the reader is hunting, a critical warning, the verdict. If more than ~10% of a section is bold, remove most of it. Never bold whole sentences or use bold as a heading substitute. Use inline code for filenames, flags, and function names so prose emphasis and code emphasis stay distinct channels.
**Why.** Emphasis is relative and scarce: when many words are bold, none stand out and the cues themselves become noise that costs a slot.
**Example.** Before: "**The pool is exhausted because each request opens a socket and never closes it.**" → After: "The pool is **exhausted** because each request opens a socket and never closes it."

---

## Anti-patterns (the full list)

1. **Burying the lede** — opening with restated context, a definition, methodology, or "it depends" so the answer sits where scanners never reach.
2. **Throat-clearing / restated-question openers** — "Great question!", "You asked how to X. X is a common task…", "In order to understand this we first need to…". A documented AI tell, zero information.
3. **Simplification mistaken for comprehension** — removing the mechanism, example, or caveat that lets the learner transfer the idea.
4. **Answering with missing context** — guessing the learner's goal, audience, or constraints when one question would materially improve the explanation.
5. **Definition-first / abstract-first openings** — leading with a general rule before any concrete instance for a novice.
6. **Skipped steps in a worked example** — "…then configure the rest" omits exactly the steps the reader has not automated.
7. **No model check** — the answer sounds clear but gives the user no way to test whether they actually understood it.
8. **Wall of text** — multi-sentence, multi-idea paragraphs with no headings, blank lines, or lists.
9. **Flat list past ~4** with no grouping — overflows the ~4-chunk buffer so the set never coheres.
10. **Bullet soup** — every item the same shape and weight, or fragmented cause-effect reasoning that loses the logic.
11. **Redundant dual-channel restatement** — narrating exactly what an adjacent code block, table, or command already states.
12. **Forward/backward references** — "as noted above/below", footnote asides, explanations placed far from the code they describe.
13. **Prose comparison tables-in-disguise** — describing N options across M attributes in flowing sentences; and the inverse, over-tabling one-dimensional data.
14. **Generic / category-label headings** — "Background", "Overview", "Details", "Notes", "Analysis".
15. **Over-signaling** — bolding whole sentences or many phrases; when everything is emphasized, nothing is.
16. **Reflexive over-hedging / weasel words** — "may", "might", "could potentially", "in some cases", "it's worth noting" on every clause.
17. **False precision or unsupported certainty** — invented numbers, dates, citations, or "scientifically proven" claims with no specific evidence.
18. **Sycophantic validation and false balance** — conceding correct answers under pushback or manufacturing "both sides" when one side clearly wins.
19. **Curse of knowledge** — emitting the expert's compressed, abstract, jargon-dense model and assuming the reader shares its scaffolding.
20. **Jargon as a hiding place** — specialist terms left undefined, masking fuzzy understanding behind fluent text; and the inverse, over-explaining terms an expert used correctly.

---

## Why this is not dominated by subtraction

The old failure mode was an RLHF-trained model whose helpfulness habits — comprehensiveness, balance, hedging, validation, uniform structure — buried the answer and overloaded working memory. Subtraction still matters because irrelevant words create extraneous load.

The sharper failure mode for `understand` is different: a response can be short and still fail to teach. The skill should remove load that does not teach while preserving or adding the elements that do: a governing idea, the learner's prior model, causal mechanism, worked example, analogy with limits, active check, and calibrated evidence.

Use this hierarchy:

1. **Accurate and grounded** beats fluent.
2. **Comprehensible and transferable** beats merely short.
3. **Short** beats long only when both teach equally well.

---

## Research anchors

Use these as the named basis for the skill, not as decoration in normal answers.

- **Cognitive load and worked examples:** Sweller (1988), Chandler & Sweller (1991), Paas, Renkl & Sweller (2003), Atkinson et al. (2000), Renkl (2014).
- **Working memory and chunking:** Cowan (2001), Miller (1956, historically important but less precise than Cowan's ~4-chunk framing).
- **Self-explanation and elaborative interrogation:** Chi et al. (1994), Pressley et al. (1987), Dunlosky et al. (2013).
- **Retrieval practice and durable learning:** Roediger & Karpicke (2006), Karpicke & Roediger (2008).
- **Multimedia learning, signaling, and split attention:** Mayer (2009/2021), Ayres & Sweller (2014).
- **Analogy and transfer:** Gentner (1983), Gick & Holyoak (1980).
- **Feedback and formative assessment:** Hattie & Timperley (2007), Black & Wiliam (1998).
- **Technical communication and information design:** inverted pyramid / BLUF practice, plain-language guidance, Nielsen-style scanability findings; treat these as applied evidence and professional convention rather than lab-proof claims.
