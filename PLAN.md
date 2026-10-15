# PLAN.md

Progress tracker. One **next step**, always. Update this file when a step is finished —
a step isn't finished until it's written down here (see `AGENTS.md` §1).

Legend: `[ ]` todo · `[x]` done · `[~]` in progress

## Done

- [x] **0.1** Read the lab brief; captured as plain text in `docs/lab-brief.md`
- [x] **0.2** Wrote the agentic scaffolding: `AGENTS.md`, `CLAUDE.md`, `README.md`,
      `PLAN.md`, `RUNS.md`
- [x] **0.3** Confirmed the uv workflow and the pin (uv 0.12.10, no `self update`)

## Next step

> **1 — Initialise the uv project.** `uv init` at the repo root (currently no
> `pyproject.toml`), keep uv at 0.12.10, add `pytest` + `ruff` as dev deps, commit
> `pyproject.toml` and `uv.lock`, and add a `.gitignore` covering `.venv/` and
> `__pycache__/`.
>
> **Done when:** `uv run python -c "print('ok')"` prints `ok`, `uv run pytest` runs and
> reports exit code 0 (with the one smoke test below), and the lockfile is committed.

- [ ] **1.1** `uv init` + dev dependencies (`pytest`, `ruff`)
- [ ] **1.2** `.gitignore`
- [ ] **1.3** One smoke test in `tests/test_smoke.py` so `pytest` has a real target
      rather than exiting "no tests ran"

## Planned

- [ ] **2 — Corpus.** Decide what the corpus is and add it as plain text under
      `corpus/`. The three audio recordings in the parent folder are *outside* the repo
      by design; if their content is wanted, transcribe to `.md`/`.txt` — do not commit
      audio (~60 MB, would also break the plain-text rule).
- [ ] **3 — Feature 1: `lab search`** (`grep -rin`), with tests over a fixed fixture corpus
- [ ] **4 — Feature 2: `lab stats`** (`wc`-derived counts), with tests
- [ ] **5 — Model-agnostic CLI adapter** — shell out to a configurable CLI command;
      provider + command read from config, never hard-coded in the module
- [ ] **6 — Feature 3: `lab ask`** — citations limited to corpus, 3–5 files, no web
- [ ] **7 — Feature 4: `lab study`** — Markdown guide, 5–10 files, inline citations
- [ ] **8 — AI-assisted rewrite of one module + written review** → `docs/ai-review.md`
- [ ] **9 — Deliverables check** — transcript, this file as plan evidence, `RUNS.md`
      table, `AGENTS.md`

## Decisions

- **Repo root** is `lab#4`, not the nested `mlr-agent-lab/` folder. That folder holds a
  starter `hello.py`; committed as-is, and probably gets absorbed into `src/` rather than
  kept as a second top-level tree.
- **The screenshot stays out of the repo.** Decided 2026-10-15 before the first push: the
  photographed brief is course material of unclear redistribution rights, and the repo is
  public. It is gitignored, and it was never in any commit — the bytes are not recoverable
  from history. `docs/lab-brief.md` carries the content as plain text instead.
- **Deterministic first.** Features 1–2 are pure `grep`/`wc` and fully testable; they
  land before anything touches a model, so the AI-dependent part is the only risky part.
- **No RAG.** The brief calls for plain tools; search is real `grep`, no embeddings,
  no vector store, no database file.
- **uv 0.12.10 stays pinned.**

## Open questions

- [ ] Is the screenshot redistributable publicly? Repo is intended to be **public** —
      `docs/lab-brief.md` is a summary rather than a verbatim copy for that reason.
- [ ] Which model CLI backs features 3–4 on this machine (`claude` is installed at
      `~/.local/bin/claude.exe`; confirm that's the intended adapter target)?
