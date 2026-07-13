# AI Architecture — Multi-Machine System

![Architecture Diagram](ai-architecture.svg)

```
┌─────────────────────────────────────────────────────────────────┐
│                      Frankenstein                               │
│           7800X3D · RTX 5070Ti 16GB · DDR5 32GB · Ubuntu       │
│                                                                 │
│  ┌────────────────────────────────────────────────────────┐    │
│  │                    Inference                             │    │
│  │  llama-server :8888                                     │    │
│  │  Qwen3.6-35B-A3B ~123 tok/s + Qwen3.5-9B Vision        │    │
│  └────────────────────────────┬───────────────────────────┘    │
│  ┌────────────────────────────┼──────────────┐                 │
│  │         Agent Layer         │              │                 │
│  │  ┌──────────┐ ┌─────────┐  │  ┌─────────┐  │                 │
│  │  │  Hermes  │ │ Frankie │  │  │ Helios  │  │                 │
│  │  │Orchestr.│ │ Worker  │  │  │ Analyst │  │                 │
│  │  └──────────┘ └─────────┘  │  └─────────┘  │                 │
│  │  ┌──────────┐ ┌─────────┐  │  ┌─────────┐  │                 │
│  │  │ OpenCode │ │  Kanban  │  │  │Odysseus│  │                 │
│  │  │  Coder   │ │  Board   │  │  │OUI+n8n │  │                 │
│  │  └──────────┘ └─────────┘  │  └─────────┘  │                 │
│  └────────────────────────────┼──────────────┘                 │
│  ┌────────────────────────────┼──────────────┐                 │
│  │         Self-Hosted         │              │                 │
│  │  ┌──────────┐ ┌─────────┐  │              │                 │
│  │  │ Nextcloud│ │ Immich  │  │  ChromaDB    │                 │
│  │  │  :8081   │ │ (planned)│  │  Vector Store│                 │
│  │  └──────────┘ └─────────┘  │              │                 │
│  └────────────────────────────┼──────────────┘                 │
│                               │                                │
│                         Tailscale                              │
└───────────────────────────────┼────────────────────────────────┘
                                │
┌───────────────────────────────┼────────────────────────────────┐
│                    Tim        │                                 │
│          MacBook Air M2 · 16GB · macOS                         │
│                               │                                 │
│  ┌────────────────────────────┼────────────┐                   │
│  │         Agent Layer        │            │                   │
│  │  AgentTim ──── remote ─────┘            │                   │
│  │  DeepSeek V4 Flash                      │                   │
│  │  Gina Profile: briefings, summaries     │                   │
│  └─────────────────────────────────────────┘                   │
└────────────────────────────────────────────────────────────────┘
                                │
                    ┌───────────┼───────────┐
                    │           │           │
                    ▼           ▼           ▼
              ┌────────┐ ┌────────┐ ┌────────┐
              │ Phone  │ │ Laptop │ │ Other  │
              │ (via   │ │ (Tim)  │ │ Devices│
              │ Tailnet│ │        │ │        │
              └────────┘ └────────┘ └────────┘
```

## Hardware

| Machine | Specs | Role |
|---------|-------|------|
| **Frankenstein** | AMD 7800X3D · RTX 5070Ti (16GB) · DDR5 32GB | Primary server — LLMs, self-hosted services, agents |
| **Tim** | Apple M2 · 16GB unified · macOS | Portable agent host, remote inference |

## Services per Machine

### Frankenstein
| Type | Service | Port |
|------|---------|------|
| **Inference** | llama-server (Qwen3.6-35B + Qwen3.5-9B Vision) | `:8888` |
| **Vector DB** | ChromaDB | `:8100` |
| **Agent** | Hermes (Orchestrator) | — |
| **Agent** | Frankie (Worker) | — |
| **Agent** | Helios (Analyst) | — |
| **Agent** | OpenCode (Coder — local Qwen 35B) | — |
| **Orchestration** | Kanban Board (SQLite multi-agent queue) | — |
| **AI Workspace** | Odysseus (OpenWebUI + n8n) | `:7000` |
| **File Sync** | Nextcloud | `:8081` |
| **Photos** | Immich | _(planned)_ |

### Tim
| Type | Service | Notes |
|------|---------|-------|
| **Agent** | AgentTim (DeepSeek V4 Flash) | MacBook management |
| **Assistant** | Gina Profile | Briefings, summaries |

## Connectivity
- **Tailscale** mesh VPN across all nodes
- SSH both directions
- Phone and other devices access self-hosted services over the tailnet
