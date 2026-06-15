# wecko-skills

Claude Code skills by [Wecko](https://wecko.ai).

## `/closing` — clean session wrap-up

One command to run before you close a Claude Code session so nothing is lost and the next session starts clean. It:

- **Persists memory** — reviews the session for durable, non-obvious facts (decisions, gotchas, fixes, state changes, your feedback) and writes/updates memory files, deleting anything the session proved wrong.
- **Refreshes CLAUDE.md** — diffs what changed this session against your project's CLAUDE.md and applies a focused update if it's stale (branch + PR or direct commit per your repo's rules).
- **Flags loose ends** — uncommitted/untracked files (yours vs foreign), open PRs and CI state, background tasks still running, anything half-done or promised.
- **Final report** — short summary of what was persisted, whether CLAUDE.md changed, and the loose-ends list.

Pass optional notes to prioritize the wrap-up: `/closing focus on the auth refactor`.

## Install (plugin marketplace)

```
/plugin marketplace add Wecko-ai/claude-skills
/plugin install closing@wecko-skills
```

Then run `/closing` in any session.

## Install (manual, no plugins)

```bash
git clone https://github.com/Wecko-ai/claude-skills.git /tmp/wecko-skills
cp -r /tmp/wecko-skills/plugins/closing ~/.claude/skills/closing
```

Then run `/closing`.

## License

MIT
