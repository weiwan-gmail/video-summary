# How we summarize

Draft. Fill this in after the first few real videos.

1. Source (url, local file, length)
2. Category (`AI/`, `Code/`, `Talks/`, `Article/`)
3. One-paragraph gist
4. Bullet takeaways
5. Quotes / timestamps worth keeping

After a video is archived:

- Canonical Whisper transcript stays under `AI/YYYY/` (`*-transcript.md` + `.summary.md`). Do not rewrite it when building the handbook.
- The long-form handbook lives under `docs/videos/`. Layout is fixed:

  **Front:** charts, architecture, overview, time anchors (Mermaid + tables).

  **Back:** `## 全文原文` — full original transcript, segmented by content (topic shifts / 时间锚), not by every Whisper crumb. Each major section starts with that block’s first timestamp (`[MM:SS]` or `[H:MM:SS]`). Merge consecutive crumbs into readable paragraphs. Keep every spoken word; do not invent dialogue. Keep the top-of-page link to the `AI/YYYY/` ASR file.

See [README.md](README.md) for the page index.
