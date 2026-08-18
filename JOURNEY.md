# 🗺️ The Full Journey

How I went from zero code to a multi-machine, multi-agent AI system in under a year.

---

## Prologue: The Beginning (September 2025)
Moved to the UK to start my MBM (Master of Business Management) at Cardiff University. The second I got here, I saw how bad the job market was. The Institute of Student Employers reported 140 applications per graduate vacancy. Graduate hiring fell 8%. A third of all job listings were ghost jobs posted with no intent to hire. I was scared. A degree on its own wasn't going to set me apart. I needed to build something, a marketable skill that most people didn't have.

I had a gaming PC: 7800X3D, RTX 5070Ti, 32GB DDR5. Built it for games, not for AI. But it was sitting there doing nothing most of the time.

So I looked at it and thought, let me see what this thing can do.

## Phase 1: The Spark (Late 2025 / Early 2026)
Started small. Poked around whatever experimental AI tools were on the internet. Web interfaces, free tiers, anything I could get my hands on. Just seeing what these things could do.

Then I thought, can I run this on my own machine?

Found **LM Studio**. It had a GUI, a chat box right there, no terminal required. Good enough. Installed it, loaded up a tiny model, started chatting.

Had no idea what quantization meant. Didn't know what context size was. Just typed things and watched responses appear.

Most of what I learned came from **Reddit**. Searched for my GPU specs, read what other people recommended, copied their configurations, tried them out. "What model runs best on a 5070Ti?" "What quant should I use?" "Why is my context so slow?" Every setting, every decision, learned from people who'd already figured it out.

But it worked. And I wanted more.

## Phase 2: Control (Early 2026)
LM Studio was great but I wanted more. Discovered **Ollama**, and that changed everything. Suddenly I could pull any model by name from the terminal and run it instantly.

Went on a tear. Tried **Meta Llama** models. Then **Mistral**. Then **Gemma**. Then **Qwen 3.6**. Every model family felt like opening a different door, each one had its own personality, its own strengths.

This is where the obsession really took hold. Started running models on **both machines simultaneously**, Tim and Pandora, just for the fun of it. Not because I needed to. Because I could. Because it was exciting.

Had something running on Pandora's GPU while Tim chewed through a different model. Two machines, both humming, both thinking. Felt like I'd built something real.

But then I wanted the **power of my desktop with the mobility of my laptop**. Didn't want to be stuck at my desk to use AI. Wanted to use it at college, in lectures, wherever. That's when I discovered **Tailscale**. As long as both machines were on the same tailnet, I could route the endpoint and access Pandora's AI through my laptop, anywhere.

That changed everything. My laptop was no longer limited by its own hardware. It was a window into Pandora's brain.

## Phase 3: Going Deeper (Mid-2026)
Then **Open Claw** released. Was one of the early adopters, no hesitation. Factory-reset Tim, installed Open Claw, started using it. Was bewildered. Shocked, even. This was real. Running a local AI agent on my laptop.

But all of it was still running on local LLMs, models served from LM Studio on Pandora. Tim was just the interface. The brains were always local.

That realization sent me deeper. Watched long-form YouTube videos on AI deployment, LLM deployment. That's when I learned that **LM Studio and Ollama are both built on llama.cpp** underneath. So maybe I should go straight to the source.

Studied **llama.cpp**, every flag, every parameter. What each flag meant, how to tune performance. Read the docs, tried different configurations, broke things, fixed them.

Then I learned that on Apple Silicon, **vLLM** works better. So I installed **vLLM on Tim** and suddenly the MacBook wasn't just a terminal. It was a proper inference server.

- Bought **Tim** (MacBook Air M2) as a second machine
- Factory-reset Tim for Open Claw, then pivoted to Hermes
- Installed vLLM on Tim for better Apple Silicon performance
- Studied llama.cpp flags in depth

## Phase 4: Agents (March 2026 onwards)
This is where things accelerated. Discovered **Paperclip** in March and it changed how I thought about everything. Paperclip lets you run a multi-agent system as a company, with org charts, budgets, governance, and agent roles. That's when I started building **named, specialised agents for every use case**. I carefully planned the whole architecture out, not randomly.

Then I installed Hermes and it became the single biggest milestone in this entire journey. Never worked with agentic systems before. Harnesses that could push commands through the terminal, actually do tasks on the computer. This wasn't just chatting with an AI anymore. This was an AI that could *act*.

As soon as I installed Hermes, needed more and more performance out of my hardware. So I **disconnected the monitor from the GPU**. No more desktop. The GPU was now free to do nothing but inference. Dual-booted Pandora, tuned every llama.cpp flag I could find, turned the whole thing into a **headless AI server**.

Every agent, every inference, every model. I access it all **through SSH over Tailscale**. Pandora sits in a corner humming away. I never see its screen. I don't need to.

Quickly realized Open Claw was overkill for my use case. So I switched to **Hermes**, no research, no hesitation, just went for it.

### Docker

When I installed Hermes, I discovered **Docker**. Realized I could run Hermes as a Docker image, not just install it locally. That changed everything. Started running all the coding harnesses — Codex, Open Code, Claude Code — and Hermes itself inside Docker containers.

Docker keeps files safe and secure from AI APIs. API keys only live inside the containers, never on the host machine. When an agent needs a cloud model, the key stays locked inside Docker. Local inference agents never touch an API at all — they run straight off Pandora's GPU.

The inference split:
- **Hermes instances** (orchestrators) — Gemma 4 26B-A4B or Qwen 3.6 35B-A3B
- **Specialised agents** — dense local models, Qwen 3.6 27B
- **Planner and technical agent** (Super Sage) — Claude API + OpenRouter, inside Docker
- **Briefs and news** — Google Flash API hooked to a Hermes profile, inside Docker

While using Hermes, started discovering the ecosystem. So many different agents out there, nano claw, small claw, pie claw, this claw, that claw. Every week something new appeared. But Hermes was the one that stuck.

And then I hit a wall: needed **custom skills**. The built-in stuff wasn't enough. Wanted my agents to do specific things, things no one had written a skill for yet.

So I learned. Properly. Spent **two months** just learning. YouTube videos, tutorials, the Claw Hub, experimenting with Hermes day in and day out. Figured out how to write custom skills from scratch. How to package them, chain them, make agents do exactly what I needed.

### Telegram Group Chats

I have **multiple group chats with my agents on Telegram**. Each group chat is a different agent or team of agents. Hermes handles the routing. I can talk to any agent directly through its own group chat, or let Hermes orchestrate across them. It's how I manage everything from my phone — briefs come in through one chat, market updates through another, project tracking through a third. All local, all orchestrated, all accessible from anywhere.

### The Named Agents

Once Paperclip showed me what structured multi-agent systems could look like, I started naming and scoping every agent for a specific job:

| Agent | Machine | Role | Inference |
|-------|---------|------|-----------|
| **Hermes** | Pandora | Chief Orchestrator. Delegates tasks via Telegram group chats and WhatsApp. The brain of the operation. | Gemma 4 26B-A4B / Qwen 3.6 35B-A3B |
| **Frankie** | Pandora | Worker. Picks up tasks from the Kanban queue and executes them. | Qwen 3.6 27B |
| **Helios** | Pandora | Analyst. Deep reasoning, research, complex problem solving. | Qwen 3.6 27B |
| **Pi** | Pandora | Specialist. Creative and niche tasks that need a lighter touch. | Qwen 3.6 27B |
| **OpenCode** | Pandora | Coder. Code review, debugging, building software. | Qwen 3.6 35B |
| **Super Sage** | Pandora | Strategic planner and troubleshooter. Uses Claude API hooked to Pi agent for deep code analysis. Analyzes problems, plans solutions, guides every other agent. The one that thinks before anyone acts. | Claude API + OpenRouter |
| **Agent Tim** | Tim | Chief Orchestrator on the MacBook. Coordinates across all Tim-based agents. | Gemma 4 26B-A4B / Qwen 3.6 35B-A3B |
| **Sentry** | Tim | Monitor. Watches for alerts, system health, watchdog tasks. | Qwen 3.6 27B |
| **Advisor** | Tim | PA agent. Takes minutes of meetings, manages my schedule. | Qwen 3.6 27B |
| **Tracker** | Tim | ClickUp agent. Task management, project tracking. | Qwen 3.6 27B |
| **Muse** | Tim | Brainstorm agent. Creative ideation, idea generation. | Qwen 3.6 27B |
| **Scout** | Tim | Job agent. Job hunting, applications, market scanning. | Qwen 3.6 27B |
| **Forge** | Tim | Builder agent. Infrastructure, deployments, automation. | Qwen 3.6 27B |
| **Ledger** | Tim | Finance agent. Personal finances, budgeting, tracking. | Qwen 3.6 27B |
| **Pulse** | Tim | Market agent. Global markets, trends, analysis. | Qwen 3.6 27B |
| **Beacon** | Tim | News agent. Global news via Google Flash API. | Google Flash API |
| **Lens** | Tim | Document agent. Document analysis, report generation. | Qwen 3.6 27B |
| **Sentinel** | Tim | Compliance agent. Industry compliance, regulatory checks. | Qwen 3.6 27B |

Each one runs locally or through Docker containers. Hermes delegates through Telegram group chats, Frankie executes, Helios reasons, Super Sage thinks and plans, Scout hunts, Advisor schedules, Beacon reads the news. Not one AI doing everything. A system of specialists.

### Building the Skills

Since Hermes already had **Telegram and WhatsApp** configured, I wrote **custom skills to let Hermes delegate tasks to the other agents**. Not just dispatching. Real orchestration. Skills for coordinating multiple agents on a single task. Skills for "sponsoring" agents, spinning one up for a specific job and pulling results back.

That's when I stumbled into **Kanban boards**. Realized I could use them to manage agent workflows, visual queues of what's running, what's done, what's blocked. Started using Kanban boards for my agents alongside learning more and more about **n8n** for automation pipelines.

But then realized something: agentic systems like Hermes were great for general tasks, but for **strictly coding**, I needed something purpose-built. Something in the scope of actual software development.

So I installed **Codex**, **Open Code**, and **Claude Code**, all three at once inside Docker containers. Hooked them all up to my local AI. Started benchmarking them side by side, testing which one could actually write code, review PRs, and handle real development workflows. Running all three simultaneously, comparing outputs, finding strengths and weaknesses.

That's when I stopped being a user and started being someone who could evaluate tools. Wasn't just following tutorials anymore, was making informed decisions about what worked and what didn't.

## Phase 5: Self-Hosting & Bots (July 2026)
Now I run everything myself:

| Service | What it does |
|---------|-------------|
| llama-server | Local LLMs, Qwen 3.6 35B + Qwen 3.5 9B Vision |
| ChromaDB | Vector store for RAG |
| Odysseus | OpenWebUI + n8n automation |
| Nextcloud | File sync |
| Kanban Board | Multi-agent orchestration |
| 6x Agents on Pandora | Hermes, Frankie, Helios, Pi, OpenCode, Super Sage |
| 11x Agents on Tim | Agent Tim, Sentry, Advisor, Tracker, Muse, Scout, Forge, Ledger, Pulse, Beacon, Lens, Sentinel |
| Tailscale | All machines connected |

- Started building bots that could answer questions from uploaded files
- RAG pipeline: documents, embeddings, ChromaDB, answers

## Phase 6: The Full Stack (August 2026)
Everything accelerated. Multiple bots, voice, transcription, autonomous agents.

**Tim gets serious:**
- **Multiple Hermes profiles**, each with a role
- **Voice** — TTS + wake word detection
- **Live transcription** — BlackHole audio routing + Whisper STT
- **Meeting pipeline** — Teams VTT transcripts to Minutes of Meeting documents
- **Computer use** — background desktop control (clicking, typing, screenshots)
- **Browser automation** — web tasks
- **Apple integrations** — Notes, Reminders, iMessage, Find My

**Pandora grows:**
- All specialised agents run on Qwen 3.6 27B
- Hermes instances use Gemma 4 26B-A4B or Qwen 3.6 35B-A3B
- Planner and technical agent use Claude API + OpenRouter
- Briefs and news come from Google Flash API

## Phase 7: First Real Project (Late 2026)
My professor at Cardiff gave me my first real opportunity: **build a WhatsApp RAG bot for him**. Professor Joe O'Mahoney has a lot of colleagues, CEOs and industry experts, who keep asking him about his work and concepts from his published consulting books. He wanted that automated. That's what I built.

I used my **multi-agent system** to pull it off. Hermes coordinated. The agents ran inference. The pipeline handled embeddings and retrieval. It worked. It was the greatest experience of my life. Learned more from that one project than from months of experimentation.

Everything I'd built, the headless server, the Tailscale mesh, the custom skills, the Kanban boards, it all came together for a real deliverable.

It's in **demo mode** now. The client is testing it. Once they're done, I'll run QA, make a few changes, and ship it. My first project in the UK. Built entirely on local AI.

## The Stack Today
```mermaid
graph TB
    subgraph P[Pandora · 7800X3D · 5070Ti]
        LLM[llama-server :8888]
        VEC[ChromaDB :8100]
        H[Hermes · Orchestrator<br>Gemma4 26B / Qwen3.6 35B]
        F[Frankie · Worker<br>Qwen3.6 27B]
        HE[Helios · Analyst<br>Qwen3.6 27B]
        PI[Pi · Specialist<br>Qwen3.6 27B]
        OC[OpenCode · Coder<br>Qwen3.6 35B]
        SS[Super Sage · Planner<br>Claude API + OpenRouter]
        KB[Kanban Board]
        OD[Odysseus :7000]
        NC[Nextcloud :8081]
    end
    subgraph T[Tim · MacBook M2]
        AT[Agent Tim · Orchestrator<br>Gemma4 26B / Qwen3.6 35B]
        SN[Sentry · Monitor<br>Qwen3.6 27B]
        AD[Advisor · PA<br>Qwen3.6 27B]
        TK[Tracker · ClickUp<br>Qwen3.6 27B]
        MU[Muse · Brainstorm<br>Qwen3.6 27B]
        SC[Scout · Job Hunt<br>Qwen3.6 27B]
        FO[Forge · Builder<br>Qwen3.6 27B]
        LG[Ledger · Finance<br>Qwen3.6 27B]
        PL[Pulse · Markets<br>Qwen3.6 27B]
        BC[Beacon · News<br>Google Flash]
        LN[Lens · Documents<br>Qwen3.6 27B]
        SE[Sentinel · Compliance<br>Qwen3.6 27B]
        VO[Voice + TTS]
        TR[Transcription]
        CU[Computer Use]
    end
    subgraph D[Docker Containers]
        OR[OpenRouter]
        GF[Google Flash]
        CA[Claude API]
    end
    TG[Telegram Group Chats] --- H
    TS[Tailscale] --- P
    TS --- T
    TS --- Phone
    LLM --- H
    LLM --- F
    LLM --- HE
    LLM --- PI
    LLM --- OC
    SS -->|plans & guides| H
    SS -->|analyzes code| OC
    D ---|API keys inside containers| T
```

## Lessons
- **You don't need code to start.** GUI tools (LM Studio) are good enough for discovery.
- **One GPU is enough to begin.** A 5070Ti runs 9-35B models comfortably.
- **Reddit is your first teacher.** Every config, every setting, someone already figured it out.
- **Ollama changes the game.** Pull any model by name, run it instantly.
- **Try everything.** Llama, Mistral, Gemma, Qwen, each model family teaches you something different.
- **Running two machines at once is fun.** Not always practical, but always exciting.
- **Tailscale makes it mobile.** Your desktop's power, anywhere you go.
- **SSH + Tailscale open every door.** Two machines feel like one.
- **Headless is the way.** Disconnect the monitor, dedicate the GPU to inference.
- **Docker keeps things safe.** API keys stay in containers, never on the host.
- **Paperclip changes how you think about agents.** Named agents with jobs feel different than anonymous workers.
- **Every agent needs a brain behind it.** Super Sage with Claude API changed how I do code analysis.
- **Custom skills change everything.** Once you can write your own, the possibilities multiply.
- **Telegram group chats make it real.** Talking to agents through chat feels like having a team.
- **Self-hosting is addictive.** Once you control everything, you don't want to go back.
- **Voice changes everything.** Talking to your agent feels different than typing.
- **Local AI is enough.** No cloud APIs needed when your GPU does the work.
- **Real projects teach the most.** One deliverable beats a hundred experiments.
- **Fear is a good motivator.** Being scared of the job market made me build something real.

## What's Next
- Immich (photo management), finally setting it up
- SMB file sharing between machines
- More n8n automation workflows
- Agent-to-agent communication across Tim and Pandora
- Paperclip integration, structured multi-agent company
- Whatever I learn next

---

*Started with a gaming PC, a scared student, and a question. Ended up here.*
