# wecko-skills

Claude Code skills by [Wecko](https://wecko.ai).

## `/closing` — clean session wrap-up

One command to run before you close a Claude Code session so nothing is lost and the next session starts clean. It:

- **Persists memory** — reviews the session for durable, non-obvious facts (decisions, gotchas, fixes, state changes, your feedback) and writes/updates memory files, deleting anything the session proved wrong.
- **Refreshes CLAUDE.md** — diffs what changed this session against your project's CLAUDE.md and applies a focused update if it's stale (branch + PR or direct commit per your repo's rules).
- **Flags loose ends** — uncommitted/untracked files (yours vs foreign), open PRs and CI state, background tasks still running, anything half-done or promised.
- **Final report** — short summary of what was persisted, whether CLAUDE.md changed, and the loose-ends list.

Pass optional notes to prioritize the wrap-up: `/closing focus on the auth refactor`.

## `/promptfit` — vague prompt to structured ticket, then build

Turn a one-line request into an actionable ticket before any code is written. A cheap **local** LLM does the scoping — clear acceptance criteria, explicit out-of-scope — so Claude executes against a tight spec instead of guessing.

```
/promptfit fix the login button on mobile, it doesnt respond to taps
```

It refines via the local [`@wecko-ai/promptfit`](https://github.com/Wecko-ai/promptfit) CLI (Ollama), shows you the ticket, then implements it following the acceptance criteria. If the local model isn't set up, it falls back to structuring the ticket itself and tells you how to enable the faster local path.

Optional setup for the local refiner:
```bash
npm i -g @wecko-ai/promptfit
ollama pull qwen3:8b      # or: modelfit --yes  (installs the best model for your machine)
```

## Install (plugin marketplace)

```
/plugin marketplace add Wecko-ai/claude-skills
/plugin install closing@wecko-skills
/plugin install promptfit@wecko-skills
```

Then run `/closing` or `/promptfit` in any session.

## Install (manual, no plugins)

```bash
git clone https://github.com/Wecko-ai/claude-skills.git /tmp/wecko-skills
cp -r /tmp/wecko-skills/plugins/closing   ~/.claude/skills/closing
cp -r /tmp/wecko-skills/plugins/promptfit ~/.claude/skills/promptfit
```

Then run `/closing` or `/promptfit`.

## License

MIT
