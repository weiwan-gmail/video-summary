# Notes — Anthropic loops / graphs / harness

- Source: https://x.com/Mahaximus_/status/2092670041062035853
- Original: [2026-08-26-anthropic-loops-graphs-transcript.md](2026-08-26-anthropic-loops-graphs-transcript.md)

## Gist

Anthropic 平台组的人在讲：模型已经会自己往前走，卡点不再是「把模型指到正确方向」，而是 **让它跑得更久、出错能恢复、并且安全合规**。所谓 1% 的工程，是搭一套会自我改进的系统——核心是 **loop（harness）**，再往上用不同 job 的 token 组成 **graph / strategy**。

## Takeaways

- **任务粒度变了。** 以前是「改 Excel 这几个格子」；现在是「给这家公司做 DCF，决定值不值得投」。Outcome 交给 agent，人不再逐步盯。
- **基础设施是无差异化的。** 长时 agent 的持久化、沙箱、恢复，是 distributed systems 问题。他们的做法：harness / brain 跑在耐用的 server 上，真正执行再 spawn sandbox，沙箱挂了整个 agent 不死。没有「一个 harness 打天下」。
- **Harness = 一个 loop。** 最简形态：`while True: 读用户 → 问模型 → 调工具`。变长之后才叠上：安全执行环境、会话状态、MCP 凭证注入（agent 看不到 secret）。
- **再上一层才是 graphs。** 他们叫 strategy / meta-harness：给 token 不同工作（执行 vs 评判 vs dreaming——回看旧 session、写 memory、写 skill）。agent 互相进对方的 loop。差异化在这一层，不在再写一遍 while loop。
- **自己怎么用。** Remote agents 做完就说 “remember / save to memory”；用 agent 去测自己的 agent 产品。一句话：少点按钮，多让模型把经验写回去。

## Worth keeping

| Time | Point |
| --- | --- |
| 08:27 | 问题从 harness 优化变成 infrastructure |
| 10:15 | brain 耐久 + sandbox 短命 |
| 20:29 | dreaming：回看 session，写 memory / skills |
| 21:16 | “a harness is a loop” |
| 22:49 | meta-harness / strategy，loops 互相反馈 |
| 39:25 | “remember, save to memory” 就是工作流 |
