# 🏗️ My AI Journey

> From zero code to a multi-machine, multi-agent AI system — this repo tracks every step.

I came to the UK to start my degree at Cardiff University. Pretty quickly realized a degree on its own wasn't going to cut it — I needed to learn something practical. Had a gaming PC with a decent GPU sitting there, so I thought, let me see what all the AI hype is about.

That curiosity turned into a year of tinkering, breaking stuff, learning, and building things I didn't know were possible. This repo is the map of that journey.

---

## The Path

```
Phase 1  ──  Gaming PC → "wait, this GPU is good for AI?"
Phase 2  ──  LM Studio → Ollama → Tailscale → mobility
Phase 3  ──  Open Claw → llama.cpp → vLLM → going deeper
Phase 4  ──  Hermes → custom skills → agents → Kanban → n8n
Phase 5  ──  Self-hosting everything → bots → full stack
Phase 6  ──  Voice, vision, transcription, autonomous agents
Phase 7  ──  First real project → Paperclip → structured AI company (you are here)
```

---

## Today's Architecture

![System Diagram](ai-architecture.svg)

**Two machines, one tailnet, a bunch of local AI agents, and way too many containers.**

| Machine | Specs | What it does |
|---------|-------|-------------|
| **Pandora** | 7800X3D · RTX 5070Ti · 32GB · Ubuntu | All inference, all agents, all services |
| **Tim** | MacBook Air M2 · 16GB · macOS | Portable agent host, voice, transcription |

### Pandora

| Category | Service | Details |
|----------|---------|---------|
| Inference | llama-server `:8888` | Local LLMs — Qwen 3.6 35B + Qwen 3.5 9B Vision |
| Vector DB | ChromaDB `:8100` | RAG embeddings for bots and agents |
| Agent | Hermes | Orchestrator — Qwen 3.6 35B |
| Agent | Frankie | Worker — Qwen 3.6 (lighter tasks) |
| Agent | Helios | Analyst — Qwen 3.6 35B |
| Agent | Pi | Specialist — Gemma 4 12B |
| Agent | OpenCode | Coder — Qwen 3.6 35B |
| Board | Kanban | SQLite multi-agent queue |
| Workspace | Odysseus `:7000` | OpenWebUI + n8n automation |
| Self-hosted | Nextcloud `:8081` | File sync |
| Self-hosted | Immich | Photo management (planned) |
| Bot | Professor | RAG-powered arXiv research bot |

### Tim (MacBook Air M2)

| Profile | Model | Role |
|---------|-------|------|
| Agent Tim | Local LLM | Chief orchestrator, multi-agent coordination |
| Sentry | Local LLM | Monitoring, alerts, watchdog tasks |
| + others | Qwen 3.6 / Gemma 4 | Task-dependent switching |

**Tim also runs:**
- Voice TTS + wake word detection
- Live meeting transcription (BlackHole + Whisper)
- Meeting pipeline (VTT transcripts → MoM documents)
- Computer use (background desktop control)
- Browser automation
- Apple integrations (Notes, Reminders, iMessage, Find My)

**How models get picked:** Each profile grabs Qwen 3.6 or Gemma 4 depending on what it's doing — heavy reasoning goes to the bigger model, fast lightweight stuff stays small. Everything runs locally.

All connected over **Tailscale**. I access everything through SSH, even from my laptop at college.

---

## An Agent for Every Use Case

What started as "let me try running a model" turned into specialised agents for basically everything:

| Agent | What it handles |
|-------|----------------|
| PA Agent | Meeting minutes, schedule management |
| ClickUp Agent | Task and project tracking |
| Brainstorm Agent | Creative ideation |
| Job Agent | Job hunting and applications |
| Coding Agent | Code review, debugging, building |
| Builder Agent | Infrastructure and automation |
| Finance Agent | Finances and budgeting |
| Market Agent | Global markets and trends |
| News Agent | Global news aggregation |
| Document Agent | Document analysis and reports |
| Compliance Agent | Industry compliance and regulation |

All running locally. All orchestrated together. Not one AI doing everything — a system of specialists.

---

## The Full Story

See **[JOURNEY.md](JOURNEY.md)** for the complete timeline — from running my first 7B model in LM Studio to debugging multi-agent Kanban pipelines at 2am.

---

## Highlights

- **September 2025** — Moved to the UK for my degree at Cardiff. Realized I needed to upskill.
- **February 2026** — First GGUF download. Had zero idea what a "quant" was. Learned everything from Reddit.
- **March 2026** — Discovered I could control context size. Mind blown.
- **April 2026** — Open Claw released. Factory-reset Tim, installed it immediately. Early adopter.
- **May 2026** — Open Claw was overkill. Switched to Hermes. Dived into llama.cpp flags, installed vLLM on Tim.
- **May 2026** — Disconnected the monitor from the GPU. Turned Pandora into a headless AI server. All access via SSH over Tailscale.
- **May–July 2026** — Hermes became the biggest milestone. Two months learning agentic systems, custom skills, Claw Hub. Built autonomous multi-agent pipelines.
- **July 2026** — Self-hosted services live (Nextcloud, Odysseus). First WhatsApp bot deployed.
- **August 2026** — Professor bot built (RAG from arXiv). Tim gets multiple profiles, voice, transcription, computer use.
- **September 2026** — Architecture docs rewritten. Full agent stack documented.
- **Late 2026** — Built WhatsApp RAG bot for my professor. First real project. Discovered Paperclip — hierarchical multi-agent orchestration.

---

## Projects

| Repo | What it does |
|------|-------------|
| [Professor](https://github.com/stopabidi/professor-whatsapp-bot) | RAG-powered arXiv research bot |
| [AI Architecture](https://github.com/stopabidi/ai-architecture) | This repo — system docs and diagrams |

---

*Started with a gaming PC, a new country, and a question. Ended up here.*
