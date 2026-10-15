# RUNS.md — log of AI runs

One row per run: **the model, what I asked for, how I checked the result.** Newest first.

## Filling in the model column

The `<unknown>` values below are deliberate, not laziness. Claude Code shows the model on
its `/status` screen, which I cannot read programmatically — and no config file on this
machine records it (`~/.claude/settings.json`, `~/.claude.json`, and the project
`.claude/settings*.json` contain no `model` key, so it is the provider default, which
changes over time). Guessing a model name here would put a false fact in a graded
deliverable.

**To complete this file:** run `/status` in the session, read the `Model:` line, and
paste it into the rows below. If a run happened in a different session or tool, that
run's own `/status` is the source.

## Log

| Date | Model (from `/status`) | What I asked | How I checked it |
|---|---|---|---|
| 2026-10-15 | `<unknown>` | Transcribe the lab brief from `Screenshot 2026-10-15 074002.png` into plain text. | Read the image twice at full resolution. Marked illegible passages `[?]` instead of filling them in, and recorded the transcript/transfer ambiguity explicitly. |
| 2026-10-15 | `<unknown>` | Write `AGENTS.md` working rules, load it from `CLAUDE.md`, and create `README.md`, `PLAN.md`, `RUNS.md`. | Re-read the brief against each file to confirm every listed deliverable has an owner and a plan step. **No automated check exists yet** — there are no tests to run, so this was reviewed by hand, not verified. |
| 2026-10-15 | `<unknown>` | Create the public repo `mlr-agent-lab` with `gh` and push, excluding the screenshot. | Previewed the exact upload set from a real staged index (`git add -A` + `git status --short`), not from a directory listing. Removed the PNG by amending the initial commit rather than adding a delete commit, so its bytes never reach the remote; confirmed with `git log --stat` and `git ls-files`. After pushing: re-read the file list back off the remote via `gh api`. |
| 2026-10-15 | `<unknown>` | Preview what would be uploaded to a public `mlr-agent-lab` before pushing anything. | Staged into a local repo and showed `git status --short --ignored` so nothing could be silently dropped. **Nothing pushed at that point** — stopped because redistributing the course screenshot publicly was unresolved. |
| 2026-10-15 | `<unknown>` | Install `gh` and `uv` into the user folder without administrator rights, and confirm both work. | Verified the `gh` zip's SHA-256 against the official `checksums.txt` before running the binary; confirmed it lands in `~/.local/bin`, which was already first on the user PATH. Checked `uv` with a real project (`uv init`, `uv add six==1.16.0`, `uv run`) rather than an import that could pass for the wrong reason. First attempt at this check gave a misleading error (my test asked `rich` for a `__version__` it doesn't expose) — reported as my bug, not uv's. |

## Conventions

- **Append, don't rewrite.** A row is a record of what happened, including runs that
  failed or that produced something later thrown away.
- **"How I checked" means the evidence**, not the intent. `ran uv run pytest → 12 passed`
  beats "reviewed the code". If nothing was checked, write that — an unchecked run is
  worth exactly as much as an untested function.
- **No secrets, no full transcripts, no tokens.** Prompts in summary. If the full prompt
  matters, link to it rather than pasting a blob.
- Runs that changed no files still belong here (like the preview run above).
