# How we summarize

Draft. Fill this in after the first few real videos.

1. Source (url, local file, length)
2. Category (`AI/`, `Code/`, `Talks/`, `Article/`)
3. One-paragraph gist
4. Bullet takeaways
5. Quotes / timestamps worth keeping

After a video is archived:

- Canonical **reading transcript** lives under `AI/YYYY/` (`*-transcript.md` + sibling `.summary.md`). Typeset it like the cleaned handbook `## 全文原文`: content-segmented major sections, a start timestamp before each, readable paragraphs inside, full spoken text retained. Do **not** publish Whisper crumb lines (`[mm:ss-mm:ss]` every few seconds) as the archived transcript.
- The long-form handbook lives under `docs/videos/`. Layout is fixed:

  **Front:** charts, architecture, overview, time anchors (Mermaid + tables).

  **Back:** `## 全文原文` — same segmentation rules as `AI/YYYY/*-transcript.md` (topic shifts / 时间锚, not every Whisper crumb). Each major section starts with that block’s first timestamp (`[MM:SS]` or `[H:MM:SS]`). Merge consecutive crumbs into readable paragraphs (大小段落). Keep every spoken word; do not invent dialogue. Keep the top-of-page link to the `AI/YYYY/` file. Prefer one source of truth: the AI file is the canonical reading transcript; the handbook appendix is an in-page copy synced to it.

See [README.md](README.md) for the page index.
