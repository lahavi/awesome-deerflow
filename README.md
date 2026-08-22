# Awesome DeerFlow

**DeerFlow** (Deep **E**xploration + **E**fficient **R**esearch **F**low) is ByteDance's open‑source, long‑horizon **SuperAgent harness**. A single lead agent decomposes complex goals and orchestrates **sub‑agents, skills, tools, a sandbox, long‑term memory, and a message gateway** to research, code, analyze data, and ship polished artifacts — reports, slide decks, web pages, images, and video. It's model‑agnostic, runs locally or in the cloud, and is built on **LangGraph** so you can plug it into your own infra and data.

DeerFlow **2.0** (open‑sourced **February 28, 2026**) is a ground‑up rewrite that shares no code with v1 — the fixed five‑node graph is gone, replaced by a single primary agent plus a composable skills/sub‑agent system. It hit **#1 on GitHub Trending within 24 hours** and has since grown past **80,000+ stars**.

This Awesome list collects the sharpest docs, deep dives, tutorials, and experiments so you can go from "what is DeerFlow?" to production‑grade agent workflows without reinventing the graph.

---

## What's New in 2.0

Launched **February 28, 2026**, DeerFlow 2.0 hit **#1 on GitHub Trending within 24 hours** and has since crossed **80,000+ stars** — all as a ground-up rewrite sharing no code with v1. The **v2.0.0 release** (tagged **June 25, 2026**) closed its milestone with **182 merged PRs from 40 contributors** — [official release notes here](https://github.com/bytedance/deer-flow/discussions/3795).

The biggest deltas since v1 — what to look for as you read the resources below:

- **Ground‑up rewrite** — a single primary agent replaces v1's fixed five‑node graph; v2 shares no code with v1 (the original Deep Research framework lives on the `main‑1.x` branch).
- **Skills & Tools** — Markdown‑defined skills with progressive loading and `/skill‑name` slash activation. Built‑ins cover research, report generation, slides, web pages, and image/video generation.
- **Sub‑Agents** — the lead agent spawns parallel sub‑agents, each with isolated context (including an isolated checkpointer), for concurrent work. Collapsed sub‑agent cards stream the effective model and cumulative token usage in real time, attributed back to the dispatching step.
- **Self‑updating custom agents** — agents can persist edits to their own `SOUL.md` / `config.yaml` from a normal chat, with per‑user isolation.
- **Sandbox & filesystem** — isolated code execution via pluggable providers: **Local**, **Docker**, **E2B**, or a **Kubernetes** provisioner for scaled deployments — with a working per-task filesystem (uploads/workspace/outputs).
- **Agentic browser control** — optional Playwright‑powered tools (navigate, snapshot, click, type, submit) keep a live per‑conversation browser session, with SSRF screening on navigation and private-address blocking.
- **Long‑term memory & context engineering** — persistent memory plus summarization and tool‑call recovery to keep long‑horizon runs coherent. Recent additions: a **hybrid fact‑eviction policy** and manual compaction via `/compact`.
- **Managed integrations & the Lark/Feishu skill pack** — admins install shared, read‑only skill packs once; users connect via browser OAuth ("Connect Lark") with per‑user credential isolation (0700 dirs, symlink rejection) and SHA‑verified sandbox CLI binaries. A credential‑broker sidecar is on the roadmap to keep secrets out of sandboxes entirely.
- **Extension manager** — install extensions from PyPI, Git, or local paths; extensions contribute middleware, lifecycle hooks, observers, services, and authenticated FastAPI routers.
- **MCP hardening** — OAuth flows, tool‑call timeouts, **durable background tasks** with leases/retries, and **pluggable RBAC authorization** that filters denied tools before the model ever sees them.
- **Embedded Python client (`DeerFlowClient`) + Terminal Workbench (TUI)** — drive DeerFlow directly, no HTTP/Gateway needed.
- **Multi‑modal web research** — ByteDance's **InfoQuest** search/crawl toolset, plus pluggable connectors for **Tavily**, **DuckDuckGo**, **Brave Search**, **SearXNG**, **Serper** (Google Images), **Browserless**, and **Arxiv**.
- **New models** — **StepFun** and **MiMo** reasoning models join the recommended set (**Doubao‑Seed‑2.0‑Code**, **DeepSeek v3.2**, **Kimi 2.5**); **MiniMax** covers image/video/podcast generation plus a **music‑generation skill**, and **MiniMax Code** recently landed as a native ACP agent.
- **Claude Code integration** — the `claude‑to‑deerflow` skill drives a running DeerFlow instance from the terminal.
- **IM channels** — Telegram, Slack, Discord, Feishu/Lark, WeChat, WeCom, DingTalk, and **Buzz**, including **user‑owned connections** so logged‑in users can bind their own accounts. Discord gained mention‑only mode, threads, and typing indicators; Telegram streams replies by editing a placeholder message in place.
- **Tracing & observability** — **LangSmith**, **Langfuse**, and **Monocle** (an OpenTelemetry‑based tracer purpose‑built for agentic apps that records each run end‑to‑end — LLM calls, agent steps, and all) — all three can run together.
- **Scheduled tasks & session goals** — a first‑class scheduled‑task MVP in the workspace lets runs trigger on a schedule, and the `/goal` command pins a session goal (with typed blockers) so the agent keeps a long task moving instead of stopping at a single answer.
- **SkillScan safety scanner** — a deterministic scanner that blocks high‑confidence CRITICAL findings (private keys, shell execution) before the LLM‑based contextual review; gates skill installs and agent‑edited skills.
- **Security hardening** — symlinked upload rejection, masked MCP secrets, cross‑site auth POST rejection, zip‑bomb caps on artifact previews, and restricted Docker socket mounts.
- **Ops & deployment** — one‑line agent setup, `make doctor`, `make support‑bundle`, a **Helm chart**, and production multi‑worker mode (Postgres + Redis with lease‑based run ownership, SSE delivery, and orphan recovery). ⚠️ Breaking change in v2.0.0: runs hydrate from RunStore and cancellation must come from the owning worker — cross‑worker cancels now return 409.
- **LLM Space** — the DeerFlow team's "secret weapon": a sister desktop app for prototyping agent ideas, inspecting every harness step, replaying failures, and benchmarking ([deer‑flow/llm‑space](https://github.com/deer-flow/llm-space)).
- **Docs in five languages** — English, 中文, 日本語, Français, and Русский.

---

## Contents

- [Badges](#badges)
- [Getting Started](#getting-started)
- [Core Concepts](#core-concepts)
- [Starter Flows](#starter-flows)
- [Production Setups](#production-setups)
- [Patterns & Architectures](#patterns--architectures)
- [Clients, TUI & Integrations](#clients-tui--integrations)
- [Community Content & Experiments](#community-content--experiments)
- [Contributing](#contributing)
- [License](#license)

---

## Badges

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)  
[![Stars](https://img.shields.io/github/stars/lahavi/awesome-deerflow.svg?style=social)](https://github.com/lahavi/awesome-deerflow)  
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)

---

## Getting Started

Resources to go from zero to a working DeerFlow 2.0 instance on your own machine or server.

- **Official Quickstart – bytedance/deer‑flow**  
  The canonical README and docs: install prerequisites, spin up the Python backend and Node.js web UI, run the demo flow, and use `make doctor` to verify your environment.  
  https://github.com/bytedance/deer-flow

- **Configuration Guide (uv, Node, nvm, etc.)**  
  Detailed setup guide from the official repo covering Python env management with `uv`, Node tooling, and recommended system requirements.  
  https://github.com/bytedance/deer-flow/blob/main/docs/configuration_guide.md

- **shareuhack – DeerFlow 2.0 Setup Guide (May 2026 update)**  
  Current walk‑through covering installation, DeepSeek API for budget research, and Ollama local mode.  
  https://www.shareuhack.com/en/posts/deerflow-deep-research-agent-guide-2026

- **World of AI – Local Deep Research Agent Setup**  
  Video walkthrough that installs DeerFlow from scratch, configures local models (Ollama/LM Studio), and runs real research tasks end‑to‑end.  
  https://www.youtube.com/watch?v=1yl6e4TP-ss

- **DeerFlow official site – deerflow.tech**  
  High‑level overview of DeerFlow, its deep research focus, and its multi‑agent architecture.  
  https://deerflow.tech

- **DeerFlow 2.0 setup, deployment & practical overview – deerflow.one**  
  Companion site with practical deployment notes and a deeper look at sub‑agent orchestration.  
  https://deerflow.one/en

---

## Core Concepts

How DeerFlow 2.0 actually thinks under the hood — the building blocks behind every flow below.

- **Skills & Tools System**  
  Skills are Markdown‑defined, progressively loaded capabilities activated via `/skill‑name` slashes. Built‑ins include research, report generation, slides, web pages, and image/video generation — and you can author your own. Installs and agent‑edited skills run through **SkillScan**, a deterministic safety scanner that blocks high‑confidence critical findings before execution.

- **Sub‑Agents**  
  The lead agent decomposes a goal and spawns domain‑specific sub‑agents that run in parallel, each with isolated context (and its own checkpointer), then aggregates their outputs. Real‑time token usage streams back to the sub‑agent card, attributed to the dispatching step.

- **Self‑Updating Custom Agents**  
  Custom agents persist edits to their own `SOUL.md` / `config.yaml` straight from a normal chat, with per‑user isolation — the agent refines its own persona and configuration over time.

- **Sandbox & Filesystem**  
  Isolated code execution through pluggable providers — **Local**, **Docker**, **E2B**, or a **Kubernetes** provisioner for scaled deployments — with a working per‑task filesystem (uploads, workspace, outputs) the agent can read, write, grep, and diff.

- **Agentic Browser Control**  
  An optional Playwright‑powered tool group keeps a live, per‑conversation browser session: navigate, snapshot pages into stable element refs, click, type, and submit forms. Navigation goes through SSRF screening, and CDP attach fails closed unless explicitly acknowledged.

- **Managed Integrations & Extension Manager**  
  Admins install shared, read‑only **skill packs** (the Lark/Feishu CLI pack is the flagship) that users connect via browser OAuth with per‑user credential isolation. A separate extension manager installs PyPI/Git/local plugins that contribute middleware, lifecycle hooks, services, and authenticated FastAPI routers.

- **Long‑Term Memory & Context Engineering**  
  Persistent memory across runs, plus summarization and tool‑call recovery so long‑horizon tasks stay coherent instead of degrading over many steps. Use the `/goal` command to pin a session goal, and `/compact` to manually trigger context compaction when a run gets long.

- **Session Goals & Scheduled Tasks**  
  `/goal <completion condition>` pins a thread‑scoped success condition that persists across turns; scheduled tasks (`/workspace/scheduled-tasks`) run agents on time‑based, recurring, or deferred triggers.

- **InfoQuest & Multi‑Modal Search**  
  ByteDance's bundled search/crawl toolset that powers DeerFlow's web research, complemented by pluggable connectors for **Tavily**, **DuckDuckGo**, **Brave Search**, **SearXNG**, **Serper** (Google Images), **Browserless**, and **Arxiv** (academic preprints). Mix providers per‑task to balance cost, privacy, and coverage.

- **MCP Security & Authorization**  
  MCP credentials flow only through `context.secrets`, sensitive values are masked in config responses, and pluggable RBAC authorization (disabled by default) filters denied tools before the model sees them — re‑checked before every business‑tool execution.

---

## Starter Flows

Ready‑made flows that are easy to fork, tweak, and ship. In 2.0 most of these ship as **built‑in skills** rather than bespoke demo code.

- **Deep Research → Report → Slides / Podcast**  
  The flagship built‑in skill: takes a topic, performs multi‑step web research, and outputs a structured report, PowerPoint‑style deck, and optional podcast audio.

- **Document & PDF Intelligence**  
  Examples showing how DeerFlow ingests long PDFs or docs, builds retrieval over them, and then answers questions or synthesizes reports on top.

- **Code & Repo Analysis**  
  Templates where the agent reads a codebase and produces overviews, refactor suggestions, or API docs using the sandbox and built‑in Python execution.

---

## Production Setups

Patterns for running DeerFlow beyond a single laptop.

- **Local‑first, Air‑gapped Research**  
  Guides and demos focused on fully local LLMs (Ollama/LM Studio), RAG over private data, and no‑cloud workflows for sensitive research teams.

- **Server & Container Deployments**  
  Articles and community notes on running DeerFlow in Docker/Kubernetes — 2.0 ships a **Helm chart**, and production multi‑worker mode runs on **Postgres + Redis** with lease‑based run ownership, SSE delivery, and orphan recovery. The **Kubernetes sandbox provider** is the recommended path for scaled multi‑tenant deployments — plus wiring it into existing observability and exposing it as an internal "research API."

- **Enterprise Readiness & Governance**  
  Overviews of access control, data privacy, and human‑in‑the‑loop review for teams that want traceable, auditable research pipelines.

---

## Patterns & Architectures

Deep dives into how DeerFlow's agent model and orchestration work.

- **SuperAgent Harness & Sub‑Agents**  
  Breakdowns of how the 2.0 lead agent decomposes tasks, spawns sub‑agents with isolated context, and orchestrates tools — search, crawl, Python execution, and more.

- **LangGraph‑powered Orchestration**  
  Articles explaining the graph‑based state machine, message‑passing, and long‑horizon task handling that make DeerFlow feel "persistent" instead of prompt‑by‑prompt.

- **Human‑in‑the‑Loop Research**  
  Deep dives into plan review, editable research trees, and how humans can redirect or refine the agent mid‑flight without losing context.

- **Observability & Tracing (LangSmith / Langfuse / Monocle)**  
  Patterns for instrumenting long‑horizon runs: LangSmith and Langfuse for trace capture, and **Monocle** — DeerFlow's OpenTelemetry‑based tracer — for end‑to‑end recording of LLM calls, agent steps, and tool invocations across a run.

- **Create Your Own Deep Research Agent with DeerFlow – The Sequence Engineering**  
  Architecture‑level deep dive into DeerFlow's graph‑based orchestration, end‑to‑end research workflows, and multi‑modal outputs.  
  https://thesequence.substack.com/p/the-sequence-engineering-661-create

- **DeerFlow 2.0 puts new spin on Claw‑like agents – DeepLearning.ai / The Batch**  
  Concise technical overview of DeerFlow's LangGraph foundation, progressive skill loading, sandboxed environments, and long‑context orchestration.  
  https://www.deeplearning.ai/the-batch/deerflow-2-0-puts-new-spin-on-claw-like-agents

- **How to Manage Long‑Running Autonomous Tasks with Deer‑Flow – SitePoint**  
  Practitioner deep dive into keeping autonomous runs on the rails: context engineering, memory, sandboxing, and supervising tasks that run for minutes to hours.  
  https://www.sitepoint.com/deerflow-deep-dive-managing-longrunning-autonomous-tasks/

- **ByteDance Releases DeerFlow 2.0 – MarkTechPost**  
  Overview of 2.0 as an open‑source SuperAgent harness that orchestrates sub‑agents, memory, and sandboxes for complex tasks.  
  https://www.marktechpost.com/2026/03/09/bytedance-releases-deerflow-2-0-an-open-source-superagent-harness-that-orchestrates-sub-agents-memory-and-sandboxes-to-do-complex-tasks/

- **ByteDance Open‑Sources Deer‑Flow 2.0, Tops GitHub Trending – Pandaily**  
  Architecture diff: v2's single primary agent vs v1's fixed five‑node structure, and why it topped GitHub Trending within 24 hours.  
  https://pandaily.com/byte-dance-open-sources-deer-flow-2-0-tops-git-hub-trending

- **DeerFlow 2.0: ByteDance's Super‑Agent Harness That Ships Finished Artifacts – Till Freitag**  
  Architecture analysis of DeerFlow's six layers — channels, router, skills, sandboxes, memory, and artifacts — and the argument that the harness layer, not the model, is becoming the real product.  
  https://till-freitag.com/en/blog/deerflow-2-super-agent-harness

---

## Clients, TUI & Integrations

Ecosystem pieces that make DeerFlow plug into the rest of your stack.

- **Embedded Python Client (`DeerFlowClient`) + Terminal Workbench (TUI)**  
  Drive a running DeerFlow instance programmatically or from an interactive terminal UI — no HTTP/Gateway round‑trip required. The TUI now also exposes the scheduled‑task workspace, session goals (`/goal`), and manual compaction (`/compact`).

- **LLM Space – the team's "secret weapon" (`deer‑flow/llm‑space`)**  
  Sister desktop app from the DeerFlow team for prototyping agent ideas, inspecting each harness step, replaying failures, and benchmarking performance.  
  https://github.com/deer-flow/llm-space  
  Overview: https://hysenlabs.com/en/projects/deer-flow-llm-space

- **Native Android client (community)**  
  A community‑built native Android client that makes DeerFlow genuinely usable on a phone rather than just "openable" — showcased in discussion #4692.  
  https://github.com/bytedance/deer-flow/discussions/4692

- **Claude Code Integration (`claude‑to‑deerflow` skill)**  
  Install the skill to send research tasks and check status against a running DeerFlow instance, directly from Claude Code in the terminal.  
  https://claudemarketplaces.com/skills/bytedance/deer-flow/claude-to-deerflow

- **Model Providers & Local Runtimes**  
  Docs and guides for using open‑source models, Ollama, LM Studio, or cloud APIs. Recommended models: **Doubao‑Seed‑2.0‑Code**, **DeepSeek v3.2**, and **Kimi 2.5**, with **StepFun** and **MiMo** reasoning models also first‑class. **MiniMax** handles image/video/podcast generation plus a music‑generation skill, and **MiniMax Code** runs as a native ACP agent.

- **External Tools & MCP Servers**  
  Examples of wiring in Python execution, web scrapers, data sources, and MCP‑style servers for bespoke tools — MCP now supports OAuth flows, tool‑call timeouts, durable background tasks with leases/retries, and pluggable RBAC authorization.

- **Tracing & Observability**  
  Built‑in support for **LangSmith**, **Langfuse**, and **Monocle** — an OpenTelemetry‑based tracer for agentic applications that records each run end‑to‑end (LLM calls, agent steps, and tool invocations) for debugging and optimization. All three can run together.

- **IM Channels**  
  Run DeerFlow over chat with adapters for Telegram, Slack, Discord, Feishu/Lark, WeChat, WeCom, DingTalk, and **Buzz** — including **user‑owned connections** so logged‑in users can bind their own accounts. Discord supports mention‑only mode, threads, and typing indicators; Telegram streams replies by editing a placeholder message in place.

- **DeerFlow GitHub – bytedance/deer‑flow**  
  Core repo with source, docs, examples, and configuration guides for the full SuperAgent harness.  
  https://github.com/bytedance/deer-flow

---

## Community Content & Experiments

Cool things people are building with — and writing about — DeerFlow.

- **ByteDance DeerFlow 2.0: Docker of AI Workers – Medium**  
  Architectural framing of 2.0 as "Docker for AI workers," covering the Claude Code integration and the rewrite's design philosophy.  
  https://medium.com/data-science-in-your-pocket/bytedance-deerflow-2-0-docker-of-ai-workers-c866b4ff558f

- **ByteDance's DeerFlow gives your agent a sandbox, memory, and subagents out of the box – Medium (Creative AI Ninja)**  
  Deep dive on the three pillars — sandboxed execution, persistent memory, and sub‑agent orchestration — and why shipping them together is the real differentiator.  
  https://medium.com/@creativeaininja/bytedances-deerflow-gives-your-agent-a-sandbox-memory-and-subagents-out-of-the-box-402c0be85329

- **I Set Up ByteDance's DeerFlow 2.0 and Let It Run My Code – Medium (Synthetic Futures)**  
  Hands‑on report from letting DeerFlow run code in a Docker sandbox, with a close look at the persistent memory that tracks preferences, writing style, and project context across sessions.  
  https://medium.com/synthetic-futures/i-set-up-bytedances-deerflow-2-0-and-let-it-run-my-code-here-s-what-actually-happened-90bb201985ad

- **DeerFlow 2.0 Is Cool — But Do You Know Your Stack? – cstack.ai**  
  Where DeerFlow fits in a broader agent stack: how the SuperAgent harness model compares to adjacent tools and when to reach for it.  
  https://cstack.ai/blog/deerflow-is-cool-but-do-you-know-your-stack

- **How to Use ByteDance DeerFlow 2.0 in 2026 – apidog.com**  
  Practical 2026 guide covering setup, core features, sandbox security, model configuration, and API lifecycle integration.  
  https://apidog.com/blog/deer-flow-guide-2026/

- **DeerFlow 2.0: ByteDance's Open‑Source AI Agent Harness – Kiledjian**  
  Early‑2026 analysis of DeerFlow as one of the most visible agent releases of the year and why it matters.  
  https://kiledjian.com/2026/03/06/deerflow-bytedances-opensource-ai-agent.html

- **DeerFlow Tutorial – Open‑Source SuperAgent Harness – YouTube**  
  Walkthrough of the skills system, sub‑agents, sandbox execution, long‑term memory, and multi‑model support.  
  https://www.youtube.com/watch?v=mQn7QAs3cOM

- **YouTube – "DeerFlow 2.0: ByteDance's OpenClaw Rival"**  
  Tutorial showing DeerFlow 2.0 features and how to install it both locally and in production.  
  https://www.youtube.com/watch?v=Ju4hsnjYboM

- **YouTube – "This Free AI Agent Does 10 Hours of Research in 10 Minutes"**  
  Walkthrough of the multi‑agent framework for deep research, web search, data analysis, and asset generation.  
  https://www.youtube.com/watch?v=R22HnnwN4U4

- **DeerFlow: ByteDance's Open‑Source SuperAgent – Termdock**  
  Practical walkthrough: architecture, setup, MCP integration, Claude Code bridging, and monitoring parallel sub‑agents.  
  https://www.termdock.com/en/blog/deer-flow-bytedance-superagent

- **How to Use DeerFlow by ByteDance: Complete Guide – tosea.ai**  
  End‑to‑end guide to 2.0 covering skills, sub‑agents, sandboxed execution, and real‑world research workflows.  
  https://tosea.ai/blog/deerflow-bytedance-open-source-research-agent-guide

- **DeerFlow 2.0: ByteDance's Open‑Source AI Agent Framework – Progressive Robot**  
  Developer overview of the harness, the skill system, and the Claude Code terminal integration.  
  https://www.progressiverobot.com/2026/04/11/what-is-deerflow-2-0/

- **ByteDance DeerFlow Superagent Review – Flowtivity**  
  Comparison of DeerFlow 2.0's skill system against Claude Code, and where each fits.  
  https://flowtivity.ai/blog/bytedance-deerflow-superagent-review/

- **VentureBeat – "What is DeerFlow 2.0 and what should enterprises know?"**  
  Enterprise‑focused explainer covering architecture, long‑horizon orchestration, deployment modes (local vs Kubernetes vs cloud), and data‑sovereignty tradeoffs.  
  https://venturebeat.com/orchestration/what-is-deerflow-and-what-should-enterprises-know-about-this-new-local-ai

- **Dev.to – "DeerFlow 2.0: What It Is, How It Works, and Why Developers Should Pay Attention"**  
  Developer‑centric breakdown of the orchestrator, sub‑agents, skills system, and how DeerFlow decomposes complex prompts into parallel workflows.  
  https://dev.to/arshtechpro/deerflow-20-what-it-is-how-it-works-and-why-developers-should-pay-attention-3ip3

- **YouTube – "DeerFlow: ByteDance's Open‑Source AI Employee"**  
  Tour of 2.0 running 100% locally for research, coding, and website building.  
  https://www.youtube.com/watch?v=WMzo9ccjdrQ

- **YouTube – "ByteDance DeerFlow - Deep Research Agents with a LOCAL LLM!"**  
  First‑look tour of the GitHub repo, local LLM setup, and real‑time research/report‑generation demos.  
  https://www.youtube.com/watch?v=Ui0ovCVDYGs

- **DeerFlow 2.0 – AllClaw directory entry**  
  Curated directory profile of DeerFlow 2.0 as an MIT‑licensed multi‑agent runtime on LangGraph/LangChain, useful for comparing it against adjacent open‑source agent harnesses.  
  https://allclaw.org/entry/deerflow-2-0

- **Launch write‑ups and announcement threads**  
  Collections of X/Reddit posts, newsletters, and blog write‑ups analyzing DeerFlow's launch, strengths, and tradeoffs vs other agent frameworks. Start with the official [v2.0.0 release notes](https://github.com/bytedance/deer-flow/discussions/3795) (June 25, 2026 — 182 merged PRs, 40 contributors).

- **Showcase Projects & community experiments**  
  Community repos that use DeerFlow for niche use cases like investment research, OSINT, academic literature reviews, and product discovery. The repo's [Discussions → "Show and tell"](https://github.com/bytedance/deer-flow/discussions) board is the live feed — recent standouts include a benchmark‑first comparison of DeerFlow's web‑search providers, a portable‑memory setup in three config files, and a proposal to add OpenSandbox as a community SandboxProvider.

---

## Contributing

This list is intentionally curated, not exhaustive. To keep it genuinely *awesome*:

- Only add tools, articles, or examples you (or someone you trust) have actually used and would recommend.  
- Prefer high‑signal resources over long link dumps: fewer, better links.  
- Follow the Awesome Manifesto principles for quality and clarity.  
  https://github.com/sindresorhus/awesome/blob/main/awesome.md

**PR guidelines:**

1. Add a single new entry per PR when possible.  
2. Include name, one‑line description, and link.  
3. Add 1–2 sentences on why it's useful in a DeerFlow context.

Feel free to open issues for:

- Broken links or deprecated content.  
- New sections you think the list should cover.  
- Better descriptions for existing entries.

---

## License

Distributed under the MIT License. See `LICENSE` for more information.
