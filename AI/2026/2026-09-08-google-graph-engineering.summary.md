# Notes — Google graph engineering / GraphRAG ADK lab (Anatoli share)

- Source: https://x.com/AnatoliKopadze/status/2097380989538591155
- Original: [2026-09-08-google-graph-engineering-transcript.md](2026-09-08-google-graph-engineering-transcript.md)
- Tweet author: Anatoli Kopadze (promoter only; not a speaker on the recording)
- Speakers on video (from ASR): Annie (Google DevRel, lab host); Tilda (opening Q&A); unnamed Google instructor in the conceptual intro

## Gist

This ~60-minute Google-side recording (shared by Anatoli Kopadze) walks from **graph / harness / loop vocabulary** into a hands-on **GraphRAG-style agent** built with **Google ADK** on **Spanner** graph data. The opening segment contrasts graph engineering (you define nodes, edges, and data contracts for predictable workflows) with single loops and with looser agent swarms. From ~09:16, Annie runs a workshop lab: Cloud setup, Spanner knowledge graph, embeddings / semantic search, wiring tools into an ADK agent, then FastAPI + React + runner / session / memory so a chat UI can query the graph. Anatoli’s tweet frames it as “single agent → 24/7 system” and “graphs that improve themselves”; the spoken content is closer to **orchestration patterns + a GraphRAG lab** than to a literal self-modifying production fleet.

## Attribution (keep separate)

- **Established from transcript:** Google ADK workflow agents (sequential / parallel / loop); three agent communication mechanisms (shared session state, LLM-driven delegation, agent-as-tool); Annie’s GraphRAG lab on Spanner (semantic / hybrid / keyword search, ML.PREDICT-style embeddings, ADK web UI, runner + session/memory services).
- **Anatoli’s framing (tweet only):** “best 1 hour on graph engineering,” “from a single agent to a full 24/7 system,” chapter title “graphs that improve themselves,” and the upsell to his own graph-engineering guide. Do not treat those slogans as claims spoken by the Google speakers unless the transcript supports them.
- **Uncertain / ASR-fragile:** Exact product spellings (GraphRAG vs “GraphRack”), model names (“gemnet” / “John Nipro” ≈ Gemini), and whether the opening instructor is the same person as Annie (voices/segments suggest a conceptual duo with Tilda, then Annie’s lab).

## Takeaways

- **Graph ≠ knowledge graph here (opening).** Knowledge graphs emphasize data; graph engineering emphasizes **behavior**—what runs, in what order, with what handoff. Harness = tools/memory/guardrails around the model; loop = the agent cycle inside that harness; graph = the org-chart / workflow of agent and function nodes.
- **When to use which.** Loops fit simple “keep going until done” goals; **graphs** fit known workflows (e.g. PR review fan-out → join → router) with predictability and debuggability; **agent swarms** fit ambiguous problems where you give personalities and throw the problem at them.
- **ADK orchestration primitives.** Workflow agents: sequential (assembly line), parallel (independent fan-out), loop (retry until condition / max iterations). Communication: shared session state (whiteboard), LLM-driven delegation (coordinator routes), explicit invocation (wrap another agent as a tool / “consultant”).
- **Lab shape (Annie).** Build a GraphRAG agent that can do semantic / hybrid / keyword search over a Spanner-backed knowledge graph (survivor / skills / relationships demo), expose tools to an ADK agent, then connect a React UI through FastAPI using **runner**, **session service**, and **memory service** (lab uses in-memory session; docs also mention Vertex AI / DB-backed options).
- **GraphRAG vs plain RAG (as taught).** Embedding similarity finds nearby skills (e.g. “magic” ≈ medical training); **graph traversal** then pulls related entities (who has the skill) so the LLM gets richer context than vector hits alone.
- **Practice caveats from the recording.** Cloud Shell tokens expire (~30 min); refresh to continue. `adk web` is used for interactive debugging/tracing before the full stack run.

## Chapters (tweet labels + what the transcript actually covers)

| Time | Tweet label | Refined from transcript |
| --- | --- | --- |
| 00:00 | what graphs actually are | Harness / loop / graph vocabulary; PR-review fan-out → join → router example; graph engineering vs loop engineering vs agent swarm; ADK workflow agents + three communication mechanisms (wraps ~09:14). Speakers: instructor + Tilda. |
| 09:16 | your first working agent | Annie intro (DevRel); lab link; GraphRAG AI agent with ADK + Memory Bank (this video focuses on GraphRAG/ADK); Cloud / credits / env setup toward Spanner. |
| 21:15 | graph engineering explained | Why keyword/table joins fail for fuzzy skills + relationships; GraphRAG + multimodal multi-agent + Memory Bank roadmap; Spanner as unified graph store vs Neo4j/Postgres graphs; Spanner Studio visualization; embeddings / ML.PREDICT; semantic search demos. |
| 41:03 | graph engineering in practice | Step-through: service layer → semantic-search tool → ADK agent instructions + tools; GraphRAG traversal vs pure RAG; hybrid/RRF-style ranking notes; test with `adk web` (tracing, tool calls). |
| 52:21 | graphs that improve themselves | **Mismatch with tweet title:** spoken content is wiring the **full app**—runner event loop, session service, memory service, FastAPI `chat.py`, start script, React UI, 3D graph of Spanner data, live “find skills similar to Heal(y)” query. Session/memory persist conversation; not a clear “self-improving graph” demo in ASR. |

## Worth keeping

| Time | Point |
| --- | --- |
| 00:29 | Harness = everything around the model (tools, memory, guardrails); loop = agent cycle; graph = org chart of nodes |
| 01:31 | PR-review workflow: fan-out → join → router |
| 03:20 | Knowledge graph = data; graph engineering = behavior / control flow |
| 04:20 | Graph engineering: engineer defines nodes and data; high predictability for known workflows |
| 04:46 | Agent swarm: personalities + throw ambiguous problems |
| 05:50 | Workflow agents: sequential / parallel / loop |
| 06:58 | ADK communication: shared state, LLM delegation, agent-as-tool |
| 09:30 | Annie: DevRel; GraphRAG + ADK lab begins |
| 22:46 | Spanner as single source of truth for graph knowledge |
| 43:20 | GraphRAG overview: embed query, vector neighbors, then traverse graph for related context |
| 47:39 | “Successfully building a GraphRAG agent” (tools wired into ADK) |
| 50:27 | `adk web` for interactive test / tracing |
| 52:21 | Full application: connect frontend to ADK via FastAPI |
| 53:10 | Runner + session service + memory service |
| 59:55 | End-to-end: ADK + Spanner GraphRAG answering chat over the knowledge base |
