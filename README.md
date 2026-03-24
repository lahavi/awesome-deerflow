# Awesome DeerFlow

DeerFlow turns long‑horizon tasks into orchestrated agent swarms that can research, code, analyze data, and ship polished artifacts like reports, slide decks, and web pages. It’s model‑agnostic, runs locally or in the cloud, and is built on a modern LangGraph / LangChain stack so you can plug it into your own infra and data.

This Awesome list collects the sharpest docs, deep dives, tutorials, and experiments so you can go from “what is DeerFlow?” to production‑grade agent workflows without reinventing the graph.

---

## Contents

- [Badges](#badges)
- [Getting Started](#getting-started)
- [Starter Flows](#starter-flows)
- [Production Setups](#production-setups)
- [Patterns & Architectures](#patterns--architectures)
- [Integrations & Tooling](#integrations--tooling)
- [Community Content & Experiments](#community-content--experiments)
- [Contributing](#contributing)
- [License](#license)

---

## Badges

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)  
[![Stars](https://img.shields.io/github/stars/YOUR_USERNAME/awesome-deerflow.svg?style=social)](https://github.com/lahavi/awesome-deerflow)  
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](./CONTRIBUTING.md)

---

## Getting Started

Resources to go from zero to a working DeerFlow instance on your own machine or server.

- **Official Quickstart – bytedance/deer-flow**  
  The canonical README and docs: install prerequisites, spin up the Python backend and Node.js web UI, and run the demo deep‑research flow.  
  https://github.com/bytedance/deer-flow

- **World of AI – Local Deep Research Agent Setup**  
  Video walkthrough that installs DeerFlow from scratch, configures local models (Ollama/LM Studio), and runs real research tasks end‑to‑end.  
  https://www.youtube.com/watch?v=1yl6e4TP-ss

- **Configuration Guide (uv, Node, nvm, etc.)**  
  Detailed setup guide from the official repo covering Python env management with `uv`, Node tooling, and recommended system requirements.  
  https://github.com/bytedance/deer-flow/blob/main/docs/configuration_guide.md

- **DeerFlow official site – deerflow.tech**  
  High-level overview of DeerFlow, its deep research focus, and its multi‑agent architecture.  
  https://deerflow.tech

- **DeerFlow deep research companion – deerflow.net**  
  Landing page centered on the “deep research companion” experience and the Supervisor + handoffs multi‑agent design pattern.  
  https://deerflow.net

---

## Starter Flows

Ready‑made flows that are easy to fork, tweak, and ship.

- **Deep Research → Report → Slides / Podcast**  
  Official demo flow that takes a topic, performs multi‑step web research, and outputs a structured report, PowerPoint‑style deck, and optional podcast audio.  

- **Document & PDF Intelligence**  
  Examples showing how DeerFlow ingests long PDFs or docs, builds retrieval over them, and then answers questions or synthesizes reports on top.  

- **Code & Repo Analysis**  
  Templates where the agent reads a codebase and produces overviews, refactor suggestions, or API docs using the built‑in Python execution and tooling.  

---

## Production Setups

Patterns for running DeerFlow beyond a single laptop.

- **Local‑first, Air‑gapped Research**  
  Guides and demos focused on fully local LLMs, RAG over private data, and no‑cloud workflows for sensitive research teams.  

- **Server & Container Deployments**  
  Articles and community notes on running DeerFlow in Docker/Kubernetes, wiring it into existing observability, and exposing it as an internal “research API.”  

- **Enterprise Readiness & Governance**  
  Overviews of access control, data privacy, and human‑in‑the‑loop review for teams that want traceable, auditable research pipelines.  

---

## Patterns & Architectures

How DeerFlow actually thinks under the hood.

- **SuperAgent Harness & Sub‑agents**  
  Breakdowns of how the top‑level SuperAgent decomposes tasks, spawns domain‑specific sub‑agents, and uses tools like web search, crawling, and Python execution.  

- **LangGraph‑powered Orchestration**  
  Articles explaining the graph‑based state machine, message‑passing, and long‑horizon task handling that make DeerFlow feel “persistent” instead of prompt‑by‑prompt.  

- **Human‑in‑the‑Loop Research**  
  Deep dives into plan review, editable research trees, and how humans can redirect or refine the agent mid‑flight without losing context.  

- **Create Your Own Deep Research Agent with DeerFlow – The Sequence Engineering**  
  Architecture‑level deep dive into DeerFlow’s graph‑based orchestration, end‑to‑end research workflows, and multi‑modal outputs.  
  https://thesequence.substack.com/p/the-sequence-engineering-661-create

- **DeerFlow 2.0 puts new spin on Claw-like agents – DeepLearning.ai / The Batch**  
  Concise technical overview of DeerFlow’s LangGraph/LangChain foundation, progressive skill loading, sandboxed environments, and long‑context orchestration.  
  https://www.deeplearning.ai/the-batch/deerflow-2-0-puts-new-spin-on-claw-like-agents

---

## Integrations & Tooling

Ecosystem pieces that make DeerFlow plug into the rest of your stack.

- **Model Providers & Local Runtimes**  
  Docs and guides for using open‑source models, Ollama, LM Studio, or cloud APIs via LiteLLM‑style adapters in DeerFlow’s multi‑tier LLM system.  

- **External Tools & MCP Servers**  
  Examples of wiring in Python execution, web scrapers, data sources, and MCP‑style servers for bespoke tools.  

- **Monitoring & Observability**  
  Community posts and examples showing how to log runs, capture traces, and instrument agent behavior for debugging and optimization.  

- **DeerFlow GitHub – bytedance/deer-flow**  
  Core repo with source, docs, examples, and configuration guides for the full SuperAgent harness.  
  https://github.com/bytedance/deer-flow

---

## Community Content & Experiments

Cool things people are building with DeerFlow.

- **VentureBeat – “What is DeerFlow 2.0 and what should enterprises know?”**  
  Enterprise‑focused explainer covering architecture, long‑horizon orchestration, deployment modes (local vs Kubernetes vs cloud), and data‑sovereignty tradeoffs.  
  https://venturebeat.com/orchestration/what-is-deerflow-and-what-should-enterprises-know-about-this-new-local-ai

- **Dev.to – “DeerFlow 2.0: What It Is, How It Works, and Why Developers Should Pay Attention”**  
  Developer‑centric breakdown of the orchestrator, sub‑agents, skills system, and how DeerFlow decomposes complex prompts into parallel workflows.  
  https://dev.to/arshtechpro/deerflow-20-what-it-is-how-it-works-and-why-developers-should-pay-attention-3ip3

- **Launch write‑ups and announcement threads**  
  Collections of X/Reddit posts, newsletters, and blog write‑ups analyzing DeerFlow’s launch, strengths, and tradeoffs vs other agent frameworks.  

- **Open Demos & Public Instances**  
  Links to public demos or sandboxes where you can try DeerFlow in the browser without installing anything (when available).  

- **Showcase Projects**  
  Community repos that use DeerFlow for niche use cases like investment research, OSINT, academic literature reviews, and product discovery.  

- **YouTube – “ByteDance DeerFlow - Deep Research Agents with a LOCAL LLM!”**  
  First‑look tour of the GitHub repo, local LLM setup, and real‑time research/report‑generation demos.  
  https://www.youtube.com/watch?v=Ui0ovCVDYGs

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
3. Add 1–2 sentences on why it’s useful in a DeerFlow context.  

Feel free to open issues for:

- Broken links or deprecated content.  
- New sections you think the list should cover.  
- Better descriptions for existing entries.

---

## License

Distributed under the MIT License. See `LICENSE` for more information.
