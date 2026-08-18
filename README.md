# 🏗️ My AI Journey

> From zero code to a multi-machine, multi-agent AI system — this repo tracks every step.

I came to the UK to start my MBM (Master of Business Management) at Cardiff University. The second I got here, I saw how bad the job market was. The Institute of Student Employers reported 140 applications per graduate vacancy, graduate hiring fell 8%, and a third of all job listings were ghost jobs posted with no intent to hire. I was scared. A degree on its own wasn't going to set me apart. I needed to build something — a marketable skill that most people didn't have. So I looked at the gaming PC I'd brought with me and thought, let me see what this thing can do.

That curiosity turned into a year of tinkering, breaking stuff, learning, and building things I didn't know were possible. This repo is the map of that journey.

---

## The Path

```
Phase 1  ──  Gaming PC → "wait, this GPU is good for AI?"
Phase 2  ──  LM Studio → Ollama → Tailscale → mobility
Phase 3  ──  Open Claw → llama.cpp → vLLM → going deeper
Phase 4  ──  Hermes → Docker → custom skills → agents → Kanban → n8n
Phase 5  ──  Self-hosting everything → RAG bots → full stack
Phase 6  ──  Voice, vision, transcription, autonomous agents
Phase 7  ──  First real project → Paperclip → structured AI company (you are here)
```

---

## Today's Architecture

![System Diagram](ai-architecture.svg)

**Two machines, one tailnet, a multi-agent orchestration layer, Telegram group chats, and a Dockerised inference stack.**

| Machine | Specs | Role |
|---------|-------|------|
| **Pandora** | 7800X3D · RTX 5070Ti · 32GB DDR5 · Ubuntu | Headless inference server, agent orchestration, RAG pipelines, self-hosted services |
| **Tim** | MacBook Air M2 · 16GB · macOS | Portable agent host, voice interface, transcription, computer use |

### Inference Strategy

Every role gets the right model for the job. The architecture splits inference by workload type:

| Workload | Model | Rationale |
|----------|-------|-----------|
| **Orchestrators** (Hermes, Agent Tim) | Gemma 4 26B-A4B / Qwen 3.6 35B-A3B | Multi-agent delegation, task routing, complex planning |
| **Specialised agents** (Frankie, Helios, Scout, etc.) | Qwen 3.6 27B (dense local) | Domain-specific tasks, balanced quality and throughput |
| **Planner / technical agent** (Super Sage) | Claude API + OpenRouter | Deep code analysis, architectural decision-making |
| **Briefs and news** (Beacon) | Google Flash API | Fast summarisation, high-volume ingestion |

Orchestrators and coders run off Pandora's GPU via `llama-server`. Specialised agents run on dense local models. Cloud APIs (Claude, OpenRouter, Google Flash) are used selectively for tasks that benefit from frontier model capabilities. They stay locked inside Docker containers so API keys never touch the host filesystem.

### Telegram

I have **multiple group chats with my agents on Telegram**. Each group chat is a different agent or team of agents. Hermes handles the routing via custom skills that delegate tasks across the system. I can talk to any agent directly through its own group chat, or let Hermes orchestrate across them. It's a conversational interface to a multi-agent backend — manage everything from your phone.

### Pandora

| Category | Service | Details |
|----------|---------|---------|
| Inference | llama-server `:8888` | Local LLM serving — Qwen 3.6 35B (GGUF, quantised) + Qwen 3.5 9B Vision |
| Vector DB | ChromaDB `:8100` | Embedding storage for RAG pipelines |
| Board | Kanban | SQLite-backed multi-agent task queue with dependency chaining |
| Workspace | Odysseus `:7000` | OpenWebUI + n8n workflow automation |
| Self-hosted | Nextcloud `:8081` | Decentralised file sync |
| Self-hosted | Immich | Photo management (planned) |

### Named Agents

| Agent | Machine | Role | Inference |
|-------|---------|------|-----------|
| **Hermes** | Pandora | Chief Orchestrator. Multi-agent delegation via Telegram group chats and WhatsApp. Task routing, dependency resolution, skill chaining. | Gemma 4 26B-A4B / Qwen 3.6 35B-A3B |
| **Frankie** | Pandora | Worker agent. Picks up tasks from the Kanban queue, executes with tool access, reports results back. | Qwen 3.6 27B |
| **Helios** | Pandora | Analyst. Deep reasoning, research synthesis, complex problem decomposition. | Qwen 3.6 27B |
| **Pi** | Pandora | Specialist. Creative ideation, niche domain tasks, lightweight inference. | Qwen 3.6 27B |
| **OpenCode** | Pandora | Coder. Code review, debugging, refactoring, full development lifecycle. Runs inside Docker. | Qwen 3.6 35B |
| **Super Sage** | Pandora | Strategic planner and troubleshooter. Uses Claude API hooked to Pi agent for deep code analysis, architectural review, and cross-agent guidance. The system's reasoning layer. | Claude API + OpenRouter |
| **Agent Tim** | Tim | Chief Orchestrator on MacBook. Coordinates across all Tim-based agents, manages local workflows. | Gemma 4 26B-A4B / Qwen 3.6 35B-A3B |
| **Sentry** | Tim | Monitoring agent. System health checks, alert routing, watchdog tasks. | Qwen 3.6 27B |
| **Advisor** | Tim | PA agent. Meeting transcription, MoM generation, schedule management. | Qwen 3.6 27B |
| **Tracker** | Tim | Project management. ClickUp integration, task tracking, sprint planning. | Qwen 3.6 27B |
| **Muse** | Tim | Creative agent. Ideation, brainstorming, content generation. | Qwen 3.6 27B |
| **Scout** | Tim | Job market agent. Vacancy scanning, application tracking, market analysis. | Qwen 3.6 27B |
| **Forge** | Tim | Infrastructure agent. Deployment automation, server management, CI/CD pipelines. | Qwen 3.6 27B |
| **Ledger** | Tim | Finance agent. Budgeting, expense tracking, financial analysis. | Qwen 3.6 27B |
| **Pulse** | Tim | Market intelligence. Global markets, trend analysis, data synthesis. | Qwen 3.6 27B |
| **Beacon** | Tim | News agent. RSS aggregation, summarisation, daily briefings via Google Flash. | Google Flash API |
| **Lens** | Tim | Document analysis. PDF parsing, report generation, information extraction. | Qwen 3.6 27B |
| **Sentinel** | Tim | Compliance agent. Regulatory monitoring, policy analysis, audit trails. | Qwen 3.6 27B |

### Tim Capabilities
- **Voice interface** — Edge TTS + Sherpa wake word detection ("Agent Tim")
- **Live transcription** — BlackHole 2ch audio routing + Whisper STT
- **Meeting pipeline** — Microsoft Teams VTT transcript parsing → structured MoM documents
- **Computer use** — Background desktop automation via cua-driver (click, type, scroll, screenshot)
- **Browser automation** — Browser Use for web interaction tasks
- **Apple ecosystem integrations** — Notes, Reminders, iMessage, Find My via native CLIs

### Docker

I discovered Docker when I installed Hermes for the first time. I quickly realised I could run Hermes as a Docker image, not just locally. That gave me an epiphany. I started containerising all the coding harnesses (Codex, Open Code, Claude Code) and Hermes itself.

Docker provides process isolation and filesystem sandboxing. API keys for cloud services (OpenRouter, Claude, Google Flash) only live inside containers — they never touch the host machine. When a cloud model is needed, the container handles the API call, processes the response, and the key stays locked inside. Local inference agents never touch an API at all — they run straight off Pandora's GPU via the llama-server endpoint. Agents running inside the isolated containers don't get to see what's on my computer.

All connected over **Tailscale** mesh VPN. I access everything through SSH, even from my laptop at college. The tailnet provides WireGuard-based encrypted tunnels between all devices.

---

## The Full Story

See **[JOURNEY.md](JOURNEY.md)** for the complete timeline, from running my first 7B model in LM Studio to debugging multi-agent Kanban pipelines at 2am.

---

## Highlights

- **September 2025** — Moved to the UK for my MBM at Cardiff. Saw the job market. 140 applications per vacancy. Ghost jobs everywhere. Got scared. Decided to build a marketable skill.
- **November 2025** — First GGUF download. Had zero idea what quantisation was. Learned everything from Reddit.
- **December 2025** — Switched from tinkering to agentic AI. Discovered Paperclip. Started building named, specialised agents.
- **January 2026** — Open Claw released. Factory-reset Tim, installed it immediately. Early adopter.
- **February 2026** — Open Claw was overkill. Switched to Hermes. Discovered Docker. Dived into llama.cpp flags, installed vLLM on Tim.
- **February 2026** — Disconnected the monitor from the GPU. Turned Pandora into a headless AI server. All access via SSH over Tailscale.
- **February to April 2026** — Hermes became the biggest milestone. Months learning agentic systems, custom skills, Claw Hub. Built autonomous multi-agent pipelines.
- **March 2026** — Self-hosted services live (Nextcloud, Odysseus). First WhatsApp bot deployed.
- **August 2026** — AskJoe bot built for Professor Joe O'Mahoney. WhatsApp RAG bot answering questions from his published consulting work. In demo mode with the client now. Architecture docs rewritten. Full agent stack documented.

*Started with a gaming PC, a scared student, and a question. Ended up here.*
