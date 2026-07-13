# AI System Architecture

![Architecture Diagram](ai-architecture.svg)

## Machines

| Machine | Specs | What runs there |
|---------|-------|----------------|
| **Frankenstein** | 7800X3D · RTX 5070Ti · DDR5 32GB · Ubuntu | LLM inference, agents, self-hosted services |
| **Tim** | MacBook Air M2 · 16GB · macOS | Secondary agent, remote inference |

## Frankenstein

| Category | Service | Details |
|----------|---------|---------|
| Inference | llama-server `:8888` | Qwen3.6-35B-A3B (123 tok/s) + Qwen3.5-9B Vision |
| Vector DB | ChromaDB `:8100` | Embeddings, semantic retrieval |
| Agent | Hermes | Orchestrator — DeepSeek V4 Pro |
| Agent | Frankie | Worker — DeepSeek V4 Flash |
| Agent | Helios | Analyst — DeepSeek V4 Pro |
| Agent | OpenCode | Coder — Qwen 35B A3B (local) |
| Orchestration | Kanban Board | SQLite multi-agent queue |
| AI Workspace | Odysseus `:7000` | OpenWebUI + n8n |
| Self-hosted | Nextcloud `:8081` | File sync |
| Self-hosted | Immich | Photo/video (planned) |

## Tim

| Service | Notes |
|---------|-------|
| AgentTim | DeepSeek V4 Flash — MacBook management |
| Gina Profile | Daily briefings, summaries |

## Connectivity

- **Tailscale** mesh VPN connecting all nodes
- SSH both directions
- Phone accesses services via Tailscale app
