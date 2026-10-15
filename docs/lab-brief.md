# Lab brief — partial transcription

> ⚠️ **This is a summary, not a verbatim copy.** Source: `Screenshot 2026-10-15
> 074002.png` (a photo of a projected slide). Small type in the lower half is only
> partly legible, so anything below marked **[?]** needs checking against the original
> slide before you rely on it. Kept as a plain-text summary rather than a verbatim copy
> because the intended repo is **public** — see `PLAN.md` → open questions.

## Header

**MLRAI 5001 — Machine Learning Research Applications** · Lab 4
**Title: Build a Research Assistant Agent with AI tools**

## The task

Build a command-line research assistant over a small local corpus of course material.
The tool should read the corpus with ordinary tools rather than a vector database, and
anything needing a model must go through a model-agnostic CLI adapter rather than an
imported SDK.

## Features

1. **Corpus search** *(deterministic, no model)* — search the corpus with `grep`.
2. **Corpus stats** *(deterministic, no model)* — counts derived from `wc`.
3. **Ask** — answer a question from corpus files only, with file citations (roughly
   3–5 files); no web access.
4. **Study guide** — generate a Markdown study guide over a set of corpus files
   (roughly 5–10), with inline citations.

## Constraints

- Plain-text source files only.
- Model-agnostic: AI-dependent features shell out to a CLI tool; no provider SDK.
- Repo under 100 MB.

## Deliverables

- The working tool and corpus
- A transcript **[?]** — see note below
- A plan document (`PLAN.md`) as evidence of planning
- `RUNS.md`: a table of model / run / prompt
- One module rewritten with AI assistance, plus a written review of that rewrite
- An `AGENTS.md` file

> **[?] Transcript** — I read this as "transcript" (the conversation log of an agentic
> session, which is the usual artefact in this kind of lab). It could also be
> "transfer" or "transforms". Verify against the slide; if it is a transcript, it is
> probably the exported session log, which this repo does not yet have.

## Not yet captured

The lower portion of the slide appears to contain per-feature detail (exact command
names, citation limits, and whether marks are allocated per feature). It is not legible
enough to transcribe. **Do not assume the command names in `README.md` come from the
brief — they are this project's own design choice.**
