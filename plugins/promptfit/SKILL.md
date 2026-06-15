---
description: Turn a vague request into a structured ticket via a local LLM, then build it — /promptfit <your prompt>
argument-hint: <your vague prompt>
disable-model-invocation: true
---

The user invoked `/promptfit` to refine a vague request into a structured, actionable ticket BEFORE you implement it. The point: a cheap local model does the scoping work (clear acceptance criteria, explicit out-of-scope) so you execute against a tight spec instead of guessing.

The raw request is: $ARGUMENTS

## Step 1 — Pick the installed local model

promptfit defaults to `qwen3:8b`, which may not be the model the user actually pulled. First find an installed Ollama model and use it explicitly:

```bash
ollama list   # first column = model tags already on disk
```

Take the first non-`NAME` tag (e.g. `qwen3:14b-q4_K_M`) and pass it via `--model` in Step 2. If `ollama list` errors (Ollama not installed) or shows no models, skip to Step 3 (fallback) and tell the user to run `modelfit --yes` to install the best model for their machine.

## Step 2 — Refine via the local model

Run promptfit with the detected model. Try these in order and use the FIRST that works (replace `<MODEL>` with the tag from Step 1):

```bash
# A) global install (fastest)
pf '$ARGUMENTS' --model <MODEL>

# B) no global install — run via npx
npx -y @wecko-ai/promptfit '$ARGUMENTS' --model <MODEL>
```

If the current repo would help (it usually does), add file context so the ticket references real paths:
```bash
pf '$ARGUMENTS' --model <MODEL> --context path/to/relevant/file.ts
```

Capture the structured ticket from stdout. Note: reasoning models (Qwen3) think first, so a refinement can take 30-90s — that's normal. Common failures:
- `command not found` / npx cannot resolve the package → promptfit isn't available locally.
- `Cannot connect to LLM` / `ECONNREFUSED` → Ollama isn't running (`ollama serve`).
- `model ... not found` → the tag is wrong; re-check `ollama list`.

## Step 3 — If the local model is unavailable

Do NOT abort. Fall back: structure the ticket YOURSELF in the same format below (this still gives the user scoping discipline), then tell them once, briefly, how to enable the faster local path:
> Tip: install the local refiner for cheaper pre-processing — `npm i -g @wecko-ai/promptfit` and `modelfit --yes` (installs the best model for your machine).

Ticket format:
```
## Task: <clear, specific title>

### Context
- What to read first; existing patterns / CLAUDE.md to follow.

### Requirements
- What must change, specifically. Expected behavior after.

### Steps
1. <action> → verify <checkpoint>

### Acceptance Criteria
- [ ] Testable criterion (prefer a runnable command: npm test, tsc --noEmit, a curl)
- [ ] No regressions — name the check

### Do NOT
- Out of scope / over-engineering to resist
```

## Step 4 — Show, then build

1. Show the user the refined ticket (compact — title + acceptance criteria + Do NOT is enough; don't dump the whole thing if it's long).
2. If the ticket surfaced a genuine ambiguity that changes the approach, ask one tight question before coding. Otherwise proceed.
3. Implement against the ticket. Follow the acceptance criteria exactly, respect the "Do NOT" section, run the named checks, and don't expand scope beyond the ticket.

Keep it tight: the user typed one line because they wanted action, not a conversation.
