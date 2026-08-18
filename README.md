# 🏗️ My AI Journey

> From zero code to a multi-machine, multi-agent AI system — this repo tracks every step.

I came to the UK to start my degree at Cardiff University. I quickly realized a degree alone wasn't enough — I needed to upskill. I had a gaming PC. So I thought, let's try learning about AI.

That curiosity turned into a year-long spiral of tinkering, breaking, learning, and building. This repo is the map of that journey.

---

## The Path

```
Phase 1  ──  Gaming PC → "wait, this GPU is good for AI?"
Phase 2  ──  LM Studio → Ollama → Tailscale → mobility
Phase 3  ──  Open Claw → llama.cpp → vLLM → going deeper
Phase 4  ──  Hermes → custom skills → agents → Kanban → n8n
Phase 5  ──  Self-hosting everything → WhatsApp bots → full stack
Phase 6  ──  Voice, vision, transcription, autonomous agents
Phase 7  ──  First real project → Paperclip → structured AI company (you are here)
```

---

## Today's Architecture

![System Diagram](ai-architecture.svg)

**TL;DR:** Two machines, one tailnet, a handful of local AI agents, and way too many containers.

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
| Bot | WhatBot v3.5 | WhatsApp document assistant |
| Bot | WhatBot Telegram | Telegram research assistant |
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

**How models are chosen:** Each profile picks Qwen 3.6 or Gemma 4 based on what it does — reasoning-heavy tasks go to the bigger model, fast lightweight tasks stay small. Everything runs locally on the machines.

All connected over **Tailscale**. Phone accesses services through the tailnet.

---

## The Full Story

See **[JOURNEY.md](JOURNEY.md)** for the complete timeline — from running my first 7B model in LM Studio to debugging multi-agent Kanban pipelines at 2am.

---

## Highlights
- **September 2026** — Architecture documentation rewritten. Full agent stack documented.
- **Late 2026** — Built WhatsApp RAG bot for professor. First real project. Discovered Paperclip — hierarchical multi-agent orchestration.

- **September 2025** — Arrived in the UK for my degree at Cardiff University. Realized I needed to upskill.
- **February 2026** — First GGUF download. No idea what a "quant" was. Learned everything from Reddit.
- **March 2026** — Discovered I could control context size. Mind blown.
- **April 2026** — Open Claw released. Factory-reset Tim, installed it immediately. Early adopter.
- **May 2026** — Open Claw was overkill. Switched to Hermes. Studied llama.cpp flags, installed vLLM on Tim.
- **May 2026** — Disconnected monitor from GPU. Turned Pandora into a headless AI server. Dual-booted, tuned llama.cpp flags, all access via SSH over Tailscale.
- **May–July 2026** — Hermes became the biggest milestone. Two months learning agentic systems, custom skills, Claw Hub. Built autonomous multi-agent pipelines.
- **July 2026** — Self-hosted services live (Nextcloud, Odysseus). WhatBot v1 on WhatsApp.
- **August 2026** — WhatBot v3.5, Telegram bot, Professor (RAG from arXiv). Tim gets multiple profiles, voice, transcription, computer use.
- **September 2026** — Architecture documentation rewritten. Full agent stack documented.

---

## Projects

| Repo | What it does |
|------|-------------|
| [WhatBot v3.5](https://github.com/stopabidi/whatbot-v3.5) | WhatsApp document assistant — multi-format QA |
| [WhatBot Telegram](https://github.com/stopabidi/whatbot-telegram-plan) | Telegram research assistant |
| [Professor](https://github.com/stopabidi/professor-whatsapp-bot) | RAG-powered arXiv research bot |
| [WhatBot (original)](https://github.com/stopabidi/WhatBot) | First iteration — WhatsApp QA |
| [AI Architecture](https://github.com/stopabidi/ai-architecture) | This repo — system docs and diagrams |

---

*Started with a gaming PC, a new country, and a question. Ended up here.*
