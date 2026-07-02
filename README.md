# Awesome DeerFlow

**DeerFlow** (Deep **E**xploration + **E**fficient **R**esearch **F**low) is ByteDance's open‑source, long‑horizon **SuperAgent harness**. A single lead agent decomposes complex goals and orchestrates **sub‑agents, skills, tools, a sandbox, long‑term memory, and a message gateway** to research, code, analyze data, and ship polished artifacts — reports, slide decks, web pages, images, and video. It's model‑agnostic, runs locally or in the cloud, and is built on **LangGraph** so you can plug it into your own infra and data.

DeerFlow **2.0** (open‑sourced Feb 2026) is a ground‑up rewrite that shares no code with v1 — the fixed five‑node graph is gone, replaced by a single primary agent plus a composable skills/sub‑agent system.

This Awesome list collects the sharpest docs, deep dives, tutorials, and experiments so you can go from "what is DeerFlow?" to production‑grade agent workflows without reinventing the graph.

---

## What's New in 2.0

The biggest deltas since v1 — what to look for as you read the resources below:

- **Ground‑up rewrite** — a single primary agent replaces v1's fixed five‑node graph; v2 shares no code with v1.
- **Skills & Tools** — Markdown‑defined skills with progressive loading and `/skill‑name` slash activation. Built‑ins cover research, report generation, slides, web pages, and image/video generation.
- **Sub‑Agents** — the lead agent spawns parallel sub‑agents, each with isolated context, for concurrent work.
- **Sandbox & filesystem** — isolated code execution via `AioSandboxProvider`, `LocalSandboxProvider`, or a **Kubernetes** provider for scaled deployments.
- **Long‑term memory & context engineering** — persistent memory plus summarization and tool‑call recovery to keep long‑horizon runs coherent.
- **Embedded Python client (`DeerFlowClient`) + Terminal Workbench (TUI)** — drive DeerFlow directly, no HTTP/Gateway needed.
- **InfoQuest** — ByteDance's search/crawl toolset for web research.
- **Claude Code integration** — the `claude‑to‑deerflow` skill drives a running DeerFlow instance from the terminal.
- **IM channels** — Telegram, Slack, Feishu/Lark, WeChat, WeCom, and DingTalk.
- **Tracing** — LangSmith and Langfuse.
- **Ops** — one‑line agent setup, `make doctor`, `make support‑bundle`; recommended models: **Doubao‑Seed‑2.0‑Code**, **DeepSeek v3.2**, and **Kimi 2.5**.

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

---

## Core Concepts

How DeerFlow 2.0 actually thinks under the hood — the building blocks behind every flow below.

- **Skills & Tools System**  
  Skills are Markdown‑defined, progressively loaded capabilities activated via `/skill‑name` slashes. Built‑ins include research, report generation, slides, web pages, and image/video generation — and you can author your own.

- **Sub‑Agents**  
  The lead agent decomposes a goal and spawns domain‑specific sub‑agents that run in parallel, each with isolated context, then aggregates their outputs.

- **Sandbox & Filesystem**  
  Isolated code execution through pluggable providers — `AioSandboxProvider`, `LocalSandboxProvider`, or a **Kubernetes** provider for scaled deployments — with a working filesystem the agent can read and write.

- **Long‑Term Memory & Context Engineering**  
  Persistent memory across runs, plus summarization and tool‑call recovery so long‑horizon tasks stay coherent instead of degrading over many steps.

- **InfoQuest**  
  ByteDance's bundled search/crawl toolset that powers DeerFlow's web research capabilities.

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
  Articles and community notes on running DeerFlow in Docker/Kubernetes — 2.0's **Kubernetes sandbox provider** is the recommended path for scaled multi‑tenant deployments — plus wiring it into existing observability and exposing it as an internal "research API."

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

- **Create Your Own Deep Research Agent with DeerFlow – The Sequence Engineering**  
  Architecture‑level deep dive into DeerFlow's graph‑based orchestration, end‑to‑end research workflows, and multi‑modal outputs.  
  https://thesequence.substack.com/p/the-sequence-engineering-661-create

- **DeerFlow 2.0 puts new spin on Claw‑like agents – DeepLearning.ai / The Batch**  
  Concise technical overview of DeerFlow's LangGraph foundation, progressive skill loading, sandboxed environments, and long‑context orchestration.  
  https://www.deeplearning.ai/the-batch/deerflow-2-0-puts-new-spin-on-claw-like-agents

- **ByteDance Releases DeerFlow 2.0 – MarkTechPost**  
  Overview of 2.0 as an open‑source SuperAgent harness that orchestrates sub‑agents, memory, and sandboxes for complex tasks.  
  https://www.marktechpost.com/2026/03/09/bytedance-releases-deerflow-2-0-an-open-source-superagent-harness-that-orchestrates-sub-agents-memory-and-sandboxes-to-do-complex-tasks/

- **ByteDance Open‑Sources Deer‑Flow 2.0, Tops GitHub Trending – Pandaily**  
  Architecture diff: v2's single primary agent vs v1's fixed five‑node structure, and why it topped GitHub Trending within 24 hours.  
  https://pandaily.com/byte-dance-open-sources-deer-flow-2-0-tops-git-hub-trending

---

## Clients, TUI & Integrations

Ecosystem pieces that make DeerFlow plug into the rest of your stack.

- **Embedded Python Client (`DeerFlowClient`) + Terminal Workbench (TUI)**  
  Drive a running DeerFlow instance programmatically or from an interactive terminal UI — no HTTP/Gateway round‑trip required.

- **Claude Code Integration (`claude‑to‑deerflow` skill)**  
  Install the skill to send research tasks and check status against a running DeerFlow instance, directly from Claude Code in the terminal.  
  https://claudemarketplaces.com/skills/bytedance/deer-flow/claude-to-deerflow

- **Model Providers & Local Runtimes**  
  Docs and guides for using open‑source models, Ollama, LM Studio, or cloud APIs. Recommended models: **Doubao‑Seed‑2.0‑Code**, **DeepSeek v3.2**, and **Kimi 2.5**.

- **External Tools & MCP Servers**  
  Examples of wiring in Python execution, web scrapers, data sources, and MCP‑style servers for bespoke tools.

- **Tracing & Observability**  
  Built‑in support for **LangSmith** and **Langfuse** to log runs, capture traces, and instrument agent behavior for debugging and optimization.

- **IM Channels**  
  Run DeerFlow over chat with adapters for Telegram, Slack, Feishu/Lark, WeChat, WeCom, and DingTalk.

- **DeerFlow GitHub – bytedance/deer‑flow**  
  Core repo with source, docs, examples, and configuration guides for the full SuperAgent harness.  
  https://github.com/bytedance/deer-flow

---

## Community Content & Experiments

Cool things people are building with — and writing about — DeerFlow.

- **ByteDance DeerFlow 2.0: Docker of AI Workers – Medium**  
  Architectural framing of 2.0 as "Docker for AI workers," covering the Claude Code integration and the rewrite's design philosophy.  
  https://medium.com/data-science-in-your-pocket/bytedance-deerflow-2-0-docker-of-ai-workers-c866b4ff558f

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

- **Launch write‑ups and announcement threads**  
  Collections of X/Reddit posts, newsletters, and blog write‑ups analyzing DeerFlow's launch, strengths, and tradeoffs vs other agent frameworks.

- **Showcase Projects**  
  Community repos that use DeerFlow for niche use cases like investment research, OSINT, academic literature reviews, and product discovery.

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
