# video-summary — Claude Code

This repo collects **video summaries**, filed by category.

## Layout

| Path | What goes there |
| --- | --- |
| `AI/` | models, papers, product launches, research |
| `Code/` | languages, tooling, architecture, walkthroughs |
| `Talks/` | conferences, interviews, long-form that does not fit above |
| `Article/` | writeups next to a video (blog, paper notes, cleaned transcript) |
| `docs/` | durable playbooks and prompt templates |
| `memory/` | local experience log — what worked, what failed |

## How to add a summary

1. Pick a category folder.
2. One markdown file per video: `YYYY-MM-DD-short-slug.md`.
3. Start with title, source URL, length, and a 3–6 sentence gist. Then bullets. Timestamps if useful.
4. After you learn something about *how* we summarize (a prompt that worked, a length that was too long, a bad source), append it to `memory/log/YYYY-MM.md`. Promote a standing rule into `memory/profile.md` only after it has shown up more than once.

## Do not

- Commit video binaries or huge transcripts by default. Link the source.
- Invent quotes or numbers that were not in the video.
- Rewrite `memory/profile.md` on a whim; append to the log first.
