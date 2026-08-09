# wecko-skills

Claude Code skills by [Wecko](https://wecko.ai).

## `/closing` — moved to its own repo

Session wrap-up (persist memory, refresh CLAUDE.md, flag loose ends) now lives at **[Wecko-ai/closing-skill](https://github.com/Wecko-ai/closing-skill)**. Install from there.

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

## `/office` — moved to its own repo

Office mode (boss a multi-model agent roster with cross-family review) now lives at **[Wecko-ai/claude-office](https://github.com/Wecko-ai/claude-office)**. Install from there.

## Install (plugin marketplace)

```
/plugin marketplace add Wecko-ai/claude-skills
/plugin install promptfit@wecko-skills
```

Then run `/promptfit` in any session.

## Install (manual, no plugins)

```bash
git clone https://github.com/Wecko-ai/claude-skills.git /tmp/wecko-skills
cp -r /tmp/wecko-skills/plugins/promptfit ~/.claude/skills/promptfit
```

Then run `/promptfit`.

## License

MIT
