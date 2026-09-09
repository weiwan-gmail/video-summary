# Video handbook

从仓库里已归档的 transcript 拆出来的说明页，不是帖子摘要的重复。每篇对应一场视频。图用 Mermaid，在 GitHub 上直接渲染。

## 版式

前半是图和结构，后半是全文，不要反过来。

1. **前半**：概览、概念表、架构 / Mermaid、时序、时间锚、读原文注意。图表和总览靠前。
2. **后半**：`## 全文原文`。按内容分段（不要按 Whisper 每 2–4 秒一行）；每段前是该段起始时间戳 `[MM:SS]`；全文保留，不删减。语言跟 transcript 走。
3. 页顶继续链到 `AI/YYYY/` 的阅读用全文（`*-transcript.md`）。那份文件用 **同一套分段规则**（大段 + 段前起始时间戳），**不是** Whisper 碎行。手册附录是页内副本，与 AI 文件同步。

`AI/YYYY/*-transcript.md` 本身也是整理过的阅读稿：按话题切 `### [MM:SS] …`，段内大小段落，全文保留。不要把 `[mm:ss-mm:ss]` 碎行 ASR 当作已归档 transcript。

| 页 | 视频 | 核心命题 |
| --- | --- | --- |
| [Anthropic：Loops & Graphs](videos/anthropic-loops-graphs.md) | [Mahax / 41 min](https://x.com/Mahaximus_/status/2092670041062035853) | harness 是 loop；差异化在 graph / strategy |
| [GrokBot：约束与编排](videos/grokbot-workshop.md) | [0xCodila / 57 min](https://x.com/0xCodila/status/2092331579527803215) | 硬 CI 吸收 agent 的痛；每个 agent 像一个人 |
| [Google：ADK / GraphRAG](videos/google-graph-engineering.md) | [Anatoli share / 60 min](https://x.com/AnatoliKopadze/status/2097380989538591155) | 工作流图 + Spanner GraphRAG 实验；推文口号≠口播 |
| [对照](compare.md) | 对着看 | runtime / 仓库约束是一条链；graph 这个词另有三层，不要硬接成三部曲 |

原文在 `AI/2026/`：`*-transcript.md`（分段阅读稿）+ `.summary.md`。这里是二次拆解，末尾再贴一份同步的全文。
