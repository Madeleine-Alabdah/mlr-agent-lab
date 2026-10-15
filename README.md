# mlr-agent-lab

Course lab: a command-line **research assistant** for a small, local corpus of course
material — the kind of agent that reads the corpus with ordinary tools (`grep`, `wc`,
`head`) rather than a vector database. Built and documented as an *agentic* workflow:
the rules, the plan, and the log of every model run all live in this repo.

## Goal

Build `lab`, a CLI with four features, keeping the AI dependency out of the code:

| # | Feature | Command | Behaviour |
| --- | --- | --- | --- |
| 1 | Corpus search (deterministic) | `lab search <term>` | Case-insensitive search over the corpus via `grep`; prints `file:line:text` |
| 2 | Corpus stats (deterministic) | `lab stats` | `wc`-style counts: files, lines, words, per topic |
| 3 | Ask | `lab ask <question>` | Answers from corpus files only, citing 3–5 files. **No web access.** |
| 4 | Study guide | `lab study <topic>` | Markdown study guide over 5–10 corpus files, with inline file citations |

> **The command names above are ours, not the brief's.** The brief specifies four
> *behaviours* (search, stats, ask, study guide); the `lab <subcommand>` surface, the
> `src/` layout, and the choice of `pytest`/`ruff` are this project's design decisions.
> See `docs/lab-brief.md` for what the brief actually asks for.

Two further requirements from the brief: one **module must be rewritten with AI
assistance and then reviewed** (evidence in `docs/ai-review.md`), and **every model run
is logged** (`RUNS.md`).

### Design constraints (from the brief)

- **Plain-text source files only** — no notebooks as source, no binary or database
  formats. Corpus and outputs stay greppable text/JSON.
- **Model-agnostic** — features needing a model shell out to a CLI tool. No provider SDK
  imported, no model name hard-coded in a module. The provider lives in config.
- **Repo under 100 MB.**

## Status

**Nothing is implemented yet.** The repo holds the lab brief and the workflow
scaffolding (`AGENTS.md`, `PLAN.md`, `RUNS.md`). There is no CLI, no tests, and no
`pyproject.toml`. See `PLAN.md` for the order of work and the current next step.

## Setup

Requires [uv](https://docs.astral.sh/uv/). This machine is pinned to **uv 0.12.10** at
`~/.local/bin/uv` — do not upgrade it.

```bash
uv sync              # create the env from pyproject.toml + uv.lock
```

Once the project exists, everything runs through uv — never a global `pip install`:

```bash
uv run lab search "dropout"     # feature 1
uv run lab stats                # feature 2
uv run lab ask "what is X"      # feature 3
uv run lab study "attention"    # feature 4
uv add <package>                # add a dependency (updates uv.lock)
```

### Checks

```bash
uv run pytest          # tests
uv run ruff check .    # lint
```

Run both before calling anything done (`AGENTS.md` §3).

### Model configuration

Features 3–4 shell out to a configurable CLI command; nothing imports a provider SDK.
The command is set in config rather than in code — details land with `PLAN.md` step 5.
No API key is committed; anything secret lives in `.env` (gitignored).

## Repository layout

```
AGENTS.md            working rules for any AI agent — read this first
CLAUDE.md            imports AGENTS.md
PLAN.md              progress + the single next step
RUNS.md              log of model runs: model, prompt, verification
README.md            this file
docs/lab-brief.md    the lab assignment, as plain text (partial — see the note inside)
```

`mlr-agent-lab/hello.py` is a starter file that likely folds into `src/`.

The photographed brief (`Screenshot 2026-10-15 074002.png`) is **deliberately not in this
repo** — it is course material photographed off a slide, so it stays local and is
gitignored. `docs/lab-brief.md` holds the assignment as plain text, which is also what the
brief's "plain-text source files only" constraint asks for.

Planned as work lands: `corpus/`, `src/`, `tests/`.

## Working with an agent

1. Read `AGENTS.md`, then `README.md` and `PLAN.md`.
2. Python through uv only (`uv run`, `uv add`); no global pip.
3. Run the checks and show the output before claiming completion.
4. Update `PLAN.md`, and append a row to `RUNS.md` for each run.

## Deliverables

Per the brief: the working tool and corpus, a transcript, `PLAN.md` (plan evidence), a
`RUNS.md` table of model/run/prompt, the AI-assisted rewrite plus its written review,
and the `AGENTS.md` file.
