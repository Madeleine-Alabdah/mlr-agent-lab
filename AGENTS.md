# AGENTS.md — working rules

Rules for any AI agent (Claude Code, Codex, or others) working in this repository.
These apply to the whole repo. `CLAUDE.md` loads this file; other agents should read
it directly.

## 1. Orient before you change anything

Read **`README.md`** (goal, commands, constraints) and **`PLAN.md`** (current
progress, the single next step) *before* writing or editing code.

- If `PLAN.md` says an area is **done**, build on it — don't restructure it.
- Do the **next step** listed in `PLAN.md` unless I ask for something else.
- If what I ask contradicts `PLAN.md`, say so and ask before diverging.
- Update `PLAN.md` when you finish a step. A step isn't finished until it's written down.

## 2. Python goes through uv — never global pip

| Do | Don't |
| --- | --- |
| `uv run <cmd>` to execute anything | `python script.py` with a system interpreter |
| `uv add <pkg>` / `uv add --dev <pkg>` | `pip install <pkg>` |
| `uv sync` to build the env | `pip install --user`, `--system` |
| `uv run pytest`, `uv run ruff check` | bare `pytest` / `ruff` from outside the env |
| `uv lock` + committed `uv.lock` | hand-edited dependency lists |

**Never install into a global or system interpreter.** No `pip install` outside a
uv-managed environment. If a package is missing, `uv add` it and let the lockfile
record the change — don't work around it with a global install.

Pinned here: **uv 0.12.10** (`~/.local/bin/uv`). Do not run `uv self update` and do
not propose upgrading it; the version is deliberately fixed.

No administrator rights on this machine. Anything needing elevation will fail —
install user-scope into `~/.local/bin` instead.

## 3. Run checks before saying "done"

"Done" means you ran something and it passed, and you can show the output.

Before reporting completion:

1. `uv run pytest` — tests pass
2. `uv run ruff check .` — no lint errors (plus `ruff format --check .` if configured)
3. Exercise the actual command you changed, e.g.
   `uv run lab search "dropout"`, and check the output is right, not just that
   it exited 0
4. Report what you ran and what it printed — including failures, verbatim

Do not claim something works because the code looks correct. If a check failed or you
skipped one, say so explicitly. A pass you didn't run is not a pass.

## 4. Constraints from the lab brief

From the course requirements (`Screenshot 2026-10-15 074002.png`, transcribed into
`docs/lab-brief.md`):

- **Plain-text source files only.** No notebooks-as-source, no proprietary binary
  formats, no database files. The corpus and all outputs stay greppable text/JSON.
- **Model-agnostic CLI.** The AI-dependent features call a CLI tool; nothing imports a
  provider SDK or hard-codes one model. Keep provider choices in config, not in modules.
- **Repo stays under 100 MB.** Currently well under — keep it that way. Audio files in
  the *parent* folder are deliberately outside this repo; don't copy them in.

## 5. Logging

Record each substantial agent run in `RUNS.md`: model used, what was asked, how it was
verified. One row per run, newest first. No secrets, no full transcripts, no tokens.

## 6. Git

- Identity: Madeleine / madeleine.b.alabdah@gmail.com
- Commit small and often with imperative messages; never rewrite pushed history.
- Never commit secrets. `.env`, tokens, and `gh auth` material stay out of the repo.
- Don't push without being asked.
