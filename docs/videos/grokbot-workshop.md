# GrokBot：约束、CI、把 agent 编排成人

- 视频：[x.com/0xCodila/status/2092331579527803215](https://x.com/0xCodila/status/2092331579527803215)（2026-08-25，57:06）
- 原文：[transcript](../../AI/2026/2026-08-25-lauren-tan-grokbot-workshop-transcript.md) · [短摘](../../AI/2026/2026-08-25-lauren-tan-grokbot-workshop.summary.md)
- 主讲：Lauren Tan（Twitter: Potatoe）。当时 Cursor 约五个月；之前 Meta React Compiler，再往前 Netflix TL / EM。
- 片子前约 6 分钟是串进去的 React / `useEffectEvent` / compiler Q&A，她从 06:25 自我介绍开始。ASR 常把 GrokBot 听成 Grocbot / Rockbot / Glockbot。

## 他们在反什么

两头都不讨好：一头是「把思考外包给模型、一周 100 个看不懂的 PR」；另一头是人肉在 review 里当唯一护栏。Lauren 的终点是 **几乎不看代码**——但这是把仓库喂到那个程度之后的结果，不是 vibe coding 的起点。

管 agent 和管人高度同构。GrokBot 让每个 agent 有名字、有账号，像带一小队人。

绿场应用最危险：没有护栏时，你不懂的代码就不该交给 agent 控制。

## 概念分层

| 层 | 东西 | 硬还是软 | 忘了会怎样 |
| --- | --- | --- | --- |
| 形状 | 目录、特性边界、禁止的 import | 硬（静态分析 / import CI） | 编译或 CI 红 |
| 味道 | lint、禁掉的坏模式、compiler diagnostics | 硬 | CI 红 |
| 提醒 | rules、skills、style guide、Bugbot | 软 | agent 仍可能抄近路 |
| 人 | PR 评论 | 最软，且是反模式 | 下次再犯 |

原则：**shortest path is the best path**。Agent 天生抄近路，所以把正确做法做成最短的那条。

另一条：你在 PR 上重复说的那句，就该变成 lint / CI，或者直接消灭这类问题（换 API、拆模块、换语言约束）。

## 架构

```mermaid
flowchart TB
  subgraph people [人]
    LT[Lauren / 工程师]
    PM[PM / 设计 / GTM]
  end
  subgraph grok [GrokBot 编排]
    A1[Agent A<br/>有名字]
    A2[Agent B]
    A3[总结昨晚谁干了什么]
  end
  subgraph repo [仓库]
    CODE[代码]
    HARD[硬门: lint / import CI / 禁模式]
    SOFT[软门: rules / skills / Bugbot]
  end
  LT --> A1
  LT --> A2
  PM --> A1
  A1 --> CODE
  A2 --> CODE
  A3 --> LT
  CODE --> HARD
  CODE --> SOFT
  HARD -->|红则回炉| A1
  SOFT -.->|可能被忘掉| A1
```

### 框图：约束怎么叠

```mermaid
block-beta
  columns 1
  block:soft["软 · 可被忘掉"]:1
    columns 4
      R["rules"]
      SK["skills"]
      BB["Bugbot"]
      SG["style guide"]
    end
  block:hard["硬 · CI 必须红"]:1
    columns 4
      LI["lint"]
      IM["import CI"]
      BN["banned patterns"]
      CD["compiler diagnostics"]
    end
  block:human["人肉 review = 反模式，应下沉"]:1
    columns 1
      PR["PR 评论"]
    end
  soft --> hard
  hard --> human
```

她不反对 soft 层，但 **绝不只靠它**。Rust 之类「编译器很凶」的栈，在这个模型里加分：过编译 ≈ 敢信。

## 时序

### Agent 交 PR，硬门先打

```mermaid
sequenceDiagram
  participant Human
  participant Agent
  participant Repo
  participant CI as 硬 CI
  participant Soft as rules/skills/Bugbot
  Human->>Agent: 小任务（约 50 行量级）
  Agent->>Repo: 写代码（走最短路径）
  Agent->>Soft: 读规则
  Note over Soft: 可能忘、可能不稳
  Agent->>CI: push / PR
  alt lint / import / 禁模式失败
    CI-->>Agent: 红
    Agent->>Repo: 改到过
  else 过了
    CI-->>Human: 绿
    Note over Human: 不必再当人肉 linter
  end
```

### 人肉评论下沉成门

```mermaid
sequenceDiagram
  participant Rev as Reviewer
  participant PR
  participant Lint
  participant Next as 下一个 Agent
  Rev->>PR: 「别再这样写」
  Note over Rev: 每次都说 = 反模式
  Rev->>Lint: 写成规则 / CI / 消灭该类 API
  Next->>PR: 再写
  Lint-->>Next: 直接红，不必等 Lauren
```

### 一队 named agent

```mermaid
sequenceDiagram
  participant You
  participant A as Agent Lauren-night
  participant B as Agent Reviewer
  participant S as Summarizer
  participant Bot as GrokBot
  You->>A: 夜里做这块
  A->>Bot: 提交
  You->>B: 按 CI 看 A 的结果
  B->>Bot: 修 / 评
  You->>S: 总结 Lauren 昨晚干了啥
  S-->>You: 早报
```

非工程同事也能走同一条链——前提是硬门已经在。她说 GrokBot 对 GTM / 产品是「Cursor moment」：第一次能舒服地用 agent。

## 她怎么到「不看代码」

1. 先花很多 token 重构：分层、堵 import、把坏模式变成 CI。
2. PR 保持小（她举的是大约 50 行，没有硬顶）。
3. CI「烦」是特性：agent 写 GrokBot 应用时，检查是为这个栈定制的。
4. 承认实验室 token 几乎不限。对外的说法是 ROI：前期贵，若目标是 agent 写大部分代码、团队不膨胀，这账才立得住。

## 时间锚

| 时间 | 点 |
| --- | --- |
| 00:00–06:20 | 串入的 React 问答，可跳 |
| 06:25 | 自我介绍：Potatoe / compiler / Netflix EM |
| 07:24 | 管人和管 agent 同构 |
| 07:42 | 几乎不看代码，是喂仓库喂出来的 |
| 10:23 | constraints + 烦人的 CI |
| 18:16 | shortest path is the best path |
| 20:00 | 只靠 soft，仓库变垃圾 |
| 21:13 | PR 评论 → lint / CI |
| 26:08 | 每个 agent 像一个人 |

## 读原文时注意

前 6 分钟不要写进 GrokBot 架构。专有名词以口型附近的 Cursor / GrokBot / Bugbot 为准。
