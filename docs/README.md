# Video handbook

从仓库里已归档的 transcript 拆出来的说明页，不是帖子摘要的重复。每篇对应一场视频。图用 Mermaid，在 GitHub 上直接渲染。

## 版式

前半是图和结构，后半是全文，不要反过来。

1. **前半**：概览、概念表、架构 / Mermaid、时序、时间锚、读原文注意。图表和总览靠前。
2. **后半**：`## 全文原文`。按内容分段（不要按 Whisper 每 2–4 秒一行）；每段前是该段起始时间戳 `[MM:SS]`；全文保留，不删减。语言跟 transcript 走。
3. 页顶继续链到 `AI/YYYY/` 的 Whisper 行级原文（canonical ASR）。附录是页内阅读用，不是替换那些文件。

| 页 | 视频 | 核心命题 |
| --- | --- | --- |
| [Anthropic：Loops & Graphs](videos/anthropic-loops-graphs.md) | [Mahax / 41 min](https://x.com/Mahaximus_/status/2092670041062035853) | harness 是 loop；差异化在 graph / strategy |
| [GrokBot：约束与编排](videos/grokbot-workshop.md) | [0xCodila / 57 min](https://x.com/0xCodila/status/2092331579527803215) | 硬 CI 吸收 agent 的痛；每个 agent 像一个人 |
| [对照](compare.md) | 两场一起看 | 一层把 loop 跑稳，一层把仓库喂到能放手 |

行级 ASR 仍在 `AI/2026/`：`*-transcript.md` + `.summary.md`。这里是二次拆解，末尾再贴一份按内容分段的全文。
