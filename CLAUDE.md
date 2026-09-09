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
| `docs/videos/` | handbook pages: charts/architecture first, full transcript appendix last |
| `memory/` | local experience log — what worked, what failed |

## How to add a summary

1. Pick a category folder.
2. One markdown file per video: `YYYY-MM-DD-short-slug.md`.
3. Start with title, source URL, length, and a 3–6 sentence gist. Then bullets. Timestamps if useful.
4. After you learn something about *how* we summarize (a prompt that worked, a length that was too long, a bad source), append it to `memory/log/YYYY-MM.md`. Promote a standing rule into `memory/profile.md` only after it has shown up more than once.

A handbook page under `docs/videos/` is not a second gist. Front: overview, concept tables, Mermaid architecture/sequence, time anchors. Back: `## 全文原文` — full transcript, content-segmented, timestamp before each major section, no omissions. Keep linking the `AI/YYYY/` file.

Video transcripts under `AI/YYYY/*-transcript.md` must be typeset like the cleaned handbook 全文原文: content-segmented major sections with a start timestamp before each, readable paragraphs inside, full text retained. Do **not** publish Whisper crumb lines (`[mm:ss-mm:ss]` every few seconds) as the archived transcript. Handbook pages keep front charts/overview and may still append `## 全文原文` (same segmentation); keep linking the `AI/YYYY/` file.

## Do not

- Commit video binaries. Link the source. Archive the reading transcript under `AI/YYYY/`, not a Whisper crumb dump.
- Invent quotes or numbers that were not in the video.
- Rewrite `memory/profile.md` on a whim; append to the log first.
