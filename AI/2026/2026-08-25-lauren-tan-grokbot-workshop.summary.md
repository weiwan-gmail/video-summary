# Notes — Lauren Tan GrokBot workshop

- Source: https://x.com/0xCodila/status/2092331579527803215
- Original: [2026-08-25-lauren-tan-grokbot-workshop-transcript.md](2026-08-25-lauren-tan-grokbot-workshop-transcript.md)

## Gist

Lauren Tan（Twitter: Potatoe，前 Meta React / Netflix EM，当时在 Cursor 五个月）讲怎么把 GrokBot 用成「一队有名字的人」。她几乎不再看代码，不是因为 vibe coding，而是先花大量 token 把仓库改成 **连最笨的 agent 也走得通**：硬约束 + 烦人的 CI 替人扛审查。

## Takeaways

- **管 agent 像管人。** 管理经验和编排 agent 高度同构。每个 agent 一个身份、一个账号，可以互相总结对方昨晚干了什么。
- **「不看代码」是结果不是起点。** 绿场应用最危险。没有护栏时，你不懂的代码 agent 也不该有控制权。她的 PR 大概 50 行，鼓励小步。
- **软规则不够。** rules / skills / Bugbot / style guide 会忘。必须叠 **硬失败**：lint、import CI、禁掉 agent 爱抄的坏模式。人在 PR 上重复评论的那条，就该变成 CI。
- **最短路径做成最佳路径。** Agent 天生抄近路，所以把正确做法做成最短的那条。静态分析 + 编译器比人肉 review 更值得信任。
- **对非工程师也成立。** 约束够狠，PM / 设计 / GTM 也能给 GrokBot 加功能，而不用她半夜起来查 perf 回退。GrokBot 对非工程同事是「Cursor moment」。
- **Token 账。** 她承认实验室里 token 几乎不限。前期 refactor 很贵，但若目标是 agent 写大部分代码、团队保持精干，这是 ROI 问题。

## Worth keeping

| Time | Point |
| --- | --- |
| 06:25 | 自我介绍：Potatoe / React compiler / Netflix EM |
| 07:42 | 几乎不看代码，是因为先把仓库喂到那个程度 |
| 10:23 | constraints + 烦人的 CI 吸收 agent 的痛 |
| 18:16 | shortest path is the best path |
| 20:00 | 只靠 soft rules，仓库迟早变垃圾 |
| 21:13 | PR 评论 → lint / CI / 直接消灭这类问题 |
| 26:08 | 每个 agent 像一个人，一队一起编排 |
