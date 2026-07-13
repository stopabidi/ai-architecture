# 🏗️ My AI Journey

> From zero code to a multi-machine AI system — this repo tracks every step.

I had never written a line of code. Then I got curious about AI. That curiosity turned into a half-year spiral of tinkering, breaking, learning, and building. This repo is the map of that journey.

---

## The Path

```
Phase 1  ──  Gaming PC → "wait, this GPU is good for AI?"
Phase 2  ──  Ollama → LM Studio → control everything
Phase 3  ──  9B models → bigger models → multi-machine
Phase 4  ──  Agent Hermes → multi-agent orchestration
Phase 5  ──  What runs where (you are here)
```

---

## Today's Architecture

![System Diagram](ai-architecture.svg)

**TL;DR:** Two machines, one tailnet, a handful of agents, and way too many containers.

| Machine | Specs | What it does |
|---------|-------|-------------|
| **Frankenstein** | 7800X3D · RTX 5070Ti · 32GB · Ubuntu | All inference, all agents, all services |
| **Tim** | MacBook Air M2 · 16GB · macOS | Portable agent host, remote inference |

### Frankenstein

| Category | Service | Details |
|----------|---------|---------|
| Inference | llama-server `:8888` | Qwen3.6-35B (123 tok/s) + Qwen3.5-9B Vision |
| Vector DB | ChromaDB `:8100` | RAG embeddings |
| Agent | Hermes | Orchestrator — DeepSeek V4 Pro |
| Agent | Frankie | Worker — DeepSeek V4 Flash |
| Agent | Helios | Analyst — DeepSeek V4 Pro |
| Agent | OpenCode | Coder — Qwen 35B local |
| Board | Kanban | SQLite multi-agent queue |
| Workspace | Odysseus `:7000` | OpenWebUI + n8n |
| Self-hosted | Nextcloud `:8081` | File sync |
| Self-hosted | Immich | Photos (planned) |

### Tim

| Service | What |
|---------|------|
| AgentTim | DeepSeek V4 Flash — manages MacBook |
| Gina | Daily briefings, summaries |

All connected over **Tailscale**. Phone accesses services through the tailnet.

---

## The Full Story

See **[JOURNEY.md](JOURNEY.md)** for the complete timeline — from running my first 7B model in LM Studio to debugging multi-agent Kanban pipelines at 2am.

---

## Highlights

- **February 2026** — First GGUF download. No idea what a "quant" was.
- **March 2026** — Discovered I could control context size. Mind blown.
- **April 2026** — Bought a second machine just for agents.
- **May 2026** — First Hermes agent deployment.
- **June 2026** — Multi-agent Kanban orchestration working.
- **July 2026** — Self-hosted services (Nextcloud, Odysseus) live.

---

*Built by tinkering, not by knowing what I was doing.*
