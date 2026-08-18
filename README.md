# 🏗️ My AI Journey

> From zero code to a multi-machine, multi-agent AI system — this repo tracks every step.

I came to the UK to start my MBM (Master of Business Management) at Cardiff University. Second I got here, I saw how bad the job market was. The Institute of Student Employers reported 140 applications per graduate vacancy, graduate hiring fell 8%, and a third of all job listings were ghost jobs posted with no intent to hire. I was scared. A degree on its own wasn't going to set me apart. I needed to build something, a marketable skill that most people didn't have. So I looked at the gaming PC I'd brought with me and thought, let me see what this thing can do.

That curiosity turned into a year of tinkering, breaking stuff, learning, and building things I didn't know were possible. This repo is the map of that journey.

---

## The Path

```
Phase 1  ──  Gaming PC → "wait, this GPU is good for AI?"
Phase 2  ──  LM Studio → Ollama → Tailscale → mobility
Phase 3  ──  Open Claw → llama.cpp → vLLM → going deeper
Phase 4  ──  Hermes → Docker → custom skills → agents → Kanban → n8n
Phase 5  ──  Self-hosting everything → bots → full stack
Phase 6  ──  Voice, vision, transcription, autonomous agents
Phase 7  ──  First real project → Paperclip → structured AI company (you are here)
```

---

## Today's Architecture

![System Diagram](ai-architecture.svg)

**Two machines, one tailnet, a bunch of named AI agents, Telegram group chats, and way too many containers.**

| Machine | Specs | What it does |
|---------|-------|-------------|
| **Pandora** | 7800X3D · RTX 5070Ti · 32GB · Ubuntu | All inference, all agents, all services |
| **Tim** | MacBook Air M2 · 16GB · macOS | Portable agent host, voice, transcription |

### How Inference Works

Every role gets the right model for the job:

- **Hermes instances** (orchestrators) — Gemma 4 26B-A4B or Qwen 3.6 35B-A3B
- **Specialised agents** — dense local models, Qwen 3.6 27B
- **Planner and technical agent** (Super Sage) — Claude API + OpenRouter
- **Briefs and news** — Google Flash API hooked to a Hermes profile

Everything runs locally on Pandora's GPU except the planner, technical agent, and briefs profile which use cloud APIs through Docker containers. API keys only live inside containers, never on the host.

### Telegram

I have **multiple group chats with my agents on Telegram**. Each group chat is a different agent or team of agents. Hermes handles the routing. I can talk to any agent directly, or let Hermes orchestrate across them. It's how I manage everything from my phone.

### Pandora

| Category | Service | Details |
|----------|---------|---------|
| Inference | llama-server `:8888` | Local LLMs, Qwen 3.6 35B + Qwen 3.5 9B Vision |
| Vector DB | ChromaDB `:8100` | RAG embeddings for bots and agents |
| Board | Kanban | SQLite multi-agent queue |
| Workspace | Odysseus `:7000` | OpenWebUI + n8n automation |
| Self-hosted | Nextcloud `:8081` | File sync |
| Self-hosted | Immich | Photo management (planned) |

### Named Agents

| Agent | Machine | Role | Inference |
|-------|---------|------|-----------|
| **Hermes** | Pandora | Chief Orchestrator, delegates tasks via Telegram group chats and WhatsApp | Gemma 4 26B-A4B / Qwen 3.6 35B-A3B |
| **Frankie** | Pandora | Worker, handles queued tasks from Kanban board | Qwen 3.6 27B |
| **Helios** | Pandora | Analyst, deep reasoning and research | Qwen 3.6 27B |
| **Pi** | Pandora | Specialist, creative and niche tasks | Qwen 3.6 27B |
| **OpenCode** | Pandora | Coder, code review, debugging, building | Qwen 3.6 35B |
| **Super Sage** | Pandora | Strategic planner, troubleshooter, code analyst. Uses Claude API hooked to Pi agent for deep code analysis. Guides all other agents. | Claude API + OpenRouter |
| **Agent Tim** | Tim | Chief Orchestrator on MacBook, multi-agent coordination | Gemma 4 26B-A4B / Qwen 3.6 35B-A3B |
| **Sentry** | Tim | Monitor, alerts, watchdog tasks | Qwen 3.6 27B |
| **Advisor** | Tim | PA agent, meeting minutes, schedule management | Qwen 3.6 27B |
| **Tracker** | Tim | ClickUp agent, task and project tracking | Qwen 3.6 27B |
| **Muse** | Tim | Brainstorm agent, creative ideation | Qwen 3.6 27B |
| **Scout** | Tim | Job agent, job hunting, applications, market scanning | Qwen 3.6 27B |
| **Forge** | Tim | Builder agent, infrastructure, deployments, automation | Qwen 3.6 27B |
| **Ledger** | Tim | Finance agent, personal finances, budgeting | Qwen 3.6 27B |
| **Pulse** | Tim | Market agent, global markets, trends, analysis | Qwen 3.6 27B |
| **Beacon** | Tim | News agent, global news via Google Flash API | Google Flash API |
| **Lens** | Tim | Document agent, document analysis, report generation | Qwen 3.6 27B |
| **Sentinel** | Tim | Compliance agent, industry compliance, regulatory checks | Qwen 3.6 27B |

### Tim Capabilities
- Voice TTS + wake word detection ("Agent Tim")
- Live meeting transcription (BlackHole + Whisper)
- Meeting pipeline (VTT transcripts to MoM documents)
- Computer use (background desktop control)
- Browser automation
- Apple integrations (Notes, Reminders, iMessage, Find My)

### Docker

I discovered Docker when I installed Hermes for the first time. Realized I could run Hermes as a Docker image, not just locally. That changed everything. Started running all the coding harnesses (Codex, Open Code, Claude Code) and Hermes itself inside Docker containers. Keeps files safe and secure from AI APIs. API keys only live inside containers, never on the host machine.

All connected over **Tailscale**. I access everything through SSH, even from my laptop at college.

---

## The Full Story

See **[JOURNEY.md](JOURNEY.md)** for the complete timeline, from running my first 7B model in LM Studio to debugging multi-agent Kanban pipelines at 2am.

---

## Highlights

- **September 2025** — Moved to the UK for my MBM at Cardiff. Saw the job market. 140 applications per vacancy. Ghost jobs everywhere. Got scared. Decided to build a marketable skill.
- **February 2026** — First GGUF download. Had zero idea what a "quant" was. Learned everything from Reddit.
- **December 2025** — Switched from tinkering to agentic AI. Discovered Paperclip. Started building named, specialised agents.
- **Late 2025** — Discovered I could control context size. Mind blown.
- **January 2026** — Open Claw released. Factory-reset Tim, installed it immediately. Early adopter.
- **February 2026** — Open Claw was overkill. Switched to Hermes a month later. Discovered Docker. Dived into llama.cpp flags, installed vLLM on Tim.
- **February 2026** — Disconnected the monitor from the GPU. Turned Pandora into a headless AI server. All access via SSH over Tailscale.
- **February to April 2026** — Hermes became the biggest milestone. Months learning agentic systems, custom skills, Claw Hub. Built autonomous multi-agent pipelines.
- **March 2026** — Self-hosted services live (Nextcloud, Odysseus). First WhatsApp bot deployed.
- **Mid 2026** — AskJoe bot built for Professor Joe O'Mahoney. WhatsApp RAG bot answering questions from his published consulting work. In demo mode with the client now.
- **September 2026** — Architecture docs rewritten. Full agent stack documented.

---

## Projects

| Repo | What it does |
|------|-------------|
| [AskJoe](https://github.com/stopabidi/ai-architecture) | WhatsApp RAG bot for Professor Joe O'Mahoney's consulting work |
| [Professor](https://github.com/stopabidi/professor-whatsapp-bot) | RAG-powered arXiv research bot |
| [AI Architecture](https://github.com/stopabidi/ai-architecture) | This repo, system docs and diagrams |

---

*Started with a gaming PC, a scared student, and a question. Ended up here.*
