---
description: Wrap up the session before closing — persist memory, refresh CLAUDE.md, flag loose ends
argument-hint: [notes optionnelles]
disable-model-invocation: true
---

The user is about to close this session. Do a full wrap-up so nothing is lost and the next session starts clean. Work through ALL of these, then give a short final report:

## 1. Memory (auto-memory directory)
- Review what happened this session: decisions, gotchas discovered, fixes, project state changes, user feedback/corrections.
- For each durable, non-obvious fact: update the existing memory file if one covers it, else create a new one (correct frontmatter, `[[links]]`).
- Delete or rewrite memories this session proved WRONG or outdated (e.g. "X is broken" after X was fixed).
- Sync `MEMORY.md` index: one line per memory, hooks accurate, no orphan or stale entries.

## 2. CLAUDE.md freshness
- Diff what changed this session (architecture, commands, workflows, deploys, env) against project CLAUDE.md claims.
- If CLAUDE.md is stale: small focused update. If the repo requires PRs for changes, do branch + PR; if docs-only commits are fine, commit directly per project rules.

## 3. Loose ends — report, don't fix
- `git status`: uncommitted/untracked files — say which are from this session vs foreign (other tools/sessions). Never absorb foreign changes.
- Unmerged branches / open PRs created this session and their CI state.
- Background tasks/monitors still running (kill or hand off).
- Anything half-done or promised but not delivered — list explicitly with what remains.
- Known pending chores discovered this session (note them in memory if not already).

## 4. Final report
Short summary: what was persisted (memory files touched), CLAUDE.md updated or not, loose ends list. No fluff.

If the user passed notes, treat them as priorities for the wrap-up: $ARGUMENTS
