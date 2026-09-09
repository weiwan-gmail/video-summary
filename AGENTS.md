# video-summary — agent instructions

Same rules as `CLAUDE.md`. This file is the generic entry for Cursor / Codex / other agents.

- Summaries go in `AI/`, `Code/`, `Talks/`, or `Article/` — one video, one markdown file.
- Process knowledge goes in `docs/`.
- Handbook pages go in `docs/videos/`: **front** charts / architecture / overview / time anchors; **back** full original transcript (`## 全文原文`), segmented by content, timestamp before each major section, full text retained. Keep linking the `AI/YYYY/` file.
- Video transcripts under `AI/YYYY/*-transcript.md` use that same reading layout (content-segmented sections + start timestamps + readable paragraphs, full text retained). Do **not** publish Whisper crumb lines (`[mm:ss-mm:ss]` every few seconds) as the archived transcript.
- Working memory goes in `memory/`: dated log for episodes, `profile.md` for facts that should stick.
- Read `memory/profile.md` at the start of a session if you are going to write a summary. Append to `memory/log/` when you learn something.

See `CLAUDE.md` for the full table and the add-a-summary checklist.
