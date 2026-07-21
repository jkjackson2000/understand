# understand

An instruction-only skill for clear, actionable, easy-to-scan responses. It works with Codex and Claude Code.

The skill leads with what matters, keeps agent-owned work with the agent, and uses steps, examples, or visuals only when they help.

## Install

Clone once, then link it into both agents:

```bash
git clone https://github.com/jkjackson2000/understand.git ~/projects/understand
ln -s ~/projects/understand ~/.codex/skills/understand
ln -s ~/projects/understand ~/.claude/skills/understand
```

## Use by default

Add this to your shared `AGENTS.md`:

```markdown
Default to the `understand` skill for user-facing responses.
```

Invoke it directly with `$understand` in Codex or `/understand` in Claude Code.

## License

[MIT](./LICENSE) © 2026 Jared Jackson.
