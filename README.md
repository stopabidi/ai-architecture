# AI Architecture — Multi-Agent System

![Architecture Diagram](ai-architecture.svg)

```mermaid
graph TB
    subgraph Frankenstein["Frankenstein · 7800X3D · RTX 5070Ti 16GB · Ubuntu"]
        LLM[llama-server :8888<br/>Qwen3.6-35B + Qwen3.5-9B Vision]
        VEC[ChromaDB<br/>Vector Store]
        
        subgraph Agents["Agent Layer"]
            H[(Hermes)<br/>Orchestrator<br/>DeepSeek V4 Pro]
            F[Frankie<br/>Worker · DeepSeek V4 Flash]
            H2[Helios<br/>Analyst · DeepSeek V4 Pro]
            OC[OpenCode<br/>Coder · Qwen 35B local]
        end
        
        K[[Kanban Board<br/>SQLite Multi-Agent Queue]]
        
        subgraph Services["Application Layer"]
            API[FastAPI App]
            SMB[SMB Watcher]
            WA[WhatsApp Gateway]
        end
        
        O[Odysseus<br/>OpenWebUI + n8n]
    end
    
    subgraph Tim["Tim · MacBook Air M2 · 16GB"]
        AT[AgentTim<br/>DeepSeek V4 Flash]
        GP[Gina Profile<br/>Briefings · Summaries]
    end
    
    TS{{Tailscale Tailnet}}
    
    USER([Professor]) -->|Files via SMB| SMB
    USER -->|WhatsApp Query| WA
    SMB -->|Trigger| API
    API -->|Ingest| VEC
    WA -->|Query| API
    API -->|Retrieve| VEC
    API -->|Generate| LLM
    WA <-->|Reply| USER
    
    H -->|Creates| K
    K -->|Assigns| F
    K -->|Assigns| H2
    F -->|Calls| OC
    F -->|Runs| API
    H -->|Reviews| K
    
    AT -->|Remote Infer| LLM
    AT -->|SSH| Frankenstein
    
    Frankenstein --> TS
    Tim --> TS
```

A dual-machine AI infrastructure with autonomous Kanban-driven multi-agent orchestration.

## Hardware

| Machine | Specs | Role |
|---------|-------|------|
| **Frankenstein** | AMD 7800X3D · RTX 5070Ti (16GB) · DDR5 32GB | Primary compute — local LLMs, vector DB, agents |
| **Tim** | Apple M2 · 16GB unified · macOS | Portable agent host, remote inference |

## Stack

### Inference
- **llama-server** (port 8888) — Qwen3.6-35B-A3B (Q4_K_M, ~123 tok/s) + Qwen3.5-9B-UD w/ mmproj-F16 (vision)
- **ChromaDB** — vector store for RAG

### Agents (Kanban-Driven)
| Agent | Model | Role |
|-------|-------|------|
| **Hermes** | DeepSeek V4 Pro | Orchestrator — decomposes goals, links tasks, reviews handoffs |
| **Frankie** | DeepSeek V4 Flash | Worker — benchmarks, deploys, tests |
| **Helios** | DeepSeek V4 Pro | Checkpoint analyst — fix vs rebuild decisions |
| **OpenCode** | Qwen 35B A3B (local) | Coding agent — scripts, scoring, test suites |
| **AgentTim** | DeepSeek V4 Flash | MacBook management, remote inference |

### Services
- **FastAPI App** — query/ingest endpoints
- **SMB Watcher** — auto-index on file drop
- **WhatsApp Gateway** — single-number QA interface
- **Odysseus** — OpenWebUI + n8n workflow automation

### Task Pipeline
```
P0 (Prereqs) → P1 (Benchmark) → P2 (Accuracy) → P3 (Edge Cases)
                                                        ↓
                                             Helios Checkpoint
                                            /                \
                                    P4 (Soak Test)     Rebuild Path
                                            │
                                    P5 (E2E Manual)
```

### Connectivity
- **Tailscale** mesh VPN connecting all nodes
- SSH both ways, SMB share, port forwarding
