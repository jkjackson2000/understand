# Contributing to `understand`

Thanks for your interest. This skill improves fastest from real usage, so the most valuable contributions are concrete: a case where it explained something badly, a technique with stronger evidence, or a sharper before→after.

## How to contribute

Contributions come in through forks and pull requests — the standard GitHub flow:

1. **Fork** the repository to your own account.
2. **Clone** your fork and create a branch: `git checkout -b improve-worked-examples`.
3. Make your change.
4. **Push** to your fork and open a **pull request** against `main` here.

For anything larger than a typo, please **open an issue first** so we can agree on the direction before you spend time on it.

## What makes a good change

This skill is opinionated, and the opinions are load-bearing. Keep these in mind:

- **Comprehension over compression.** This is not a "make it shorter" skill. Changes that trade away mechanism, worked examples, or calibrated evidence for brevity work against its purpose.
- **Earn every rule.** A new technique in `SKILL.md` should have a corresponding entry in `references/technique-reference.md` with its rule, the cognitive principle behind it (the *why*), and a before→after. If you can't name why it helps comprehension, it probably doesn't belong.
- **Evidence, not assertion.** Prefer "research-supported" / "evidence-informed" framing over "scientifically proven." If you cite a finding, name the source in the research anchors.
- **Keep `SKILL.md` lean.** It loads on every invocation. Heavy justification goes in the reference file, not the main skill.
- **Match the existing voice** — imperative, concrete, no throat-clearing. The skill should practice what it preaches.

## Reporting a bad explanation

The single most useful issue you can file: paste a prompt, the answer the skill produced, and what would have helped you understand it better. Real failure cases are how the technique list gets sharper.

## License

By contributing, you agree that your contributions are licensed under the [MIT License](./LICENSE) that covers this project.
