# Distributed AI Mesh — 7 Nodes, One Platform

A private compute mesh spanning 7 machines (2 GPU nodes, 2 Mac workstations, a laptop, and 2 Raspberry Pis) connected over an encrypted Tailscale WireGuard network. Everything runs on local hardware — no cloud dependency for inference, storage, or orchestration.

## What It Is

A self-hosted platform for running AI workloads across heterogeneous hardware:

- **Inference** — Ollama instances across 3 nodes (2x RTX 4070 Ti SUPER + M1 Ultra), 40+ models loaded, unified gateway for routing
- **Multi-provider inference engine** — 146 models across 6 providers (Gemini, Mistral, OpenAI, Vertex AI, Ollama, Puter) with 80+ API keys and automatic rotation
- **Mesh governance** — Central API tracking jobs, node health, memories, audit trails, and inter-node communication across the entire mesh
- **Web intelligence** — Search, scrape, and analysis pipeline (multi-engine search, deep scraping with JS rendering, NLP analysis)
- **Instance chat** — Claude-to-Claude messaging system for coordinating work across nodes
- **Security** — Honeypot services, threat intelligence, key-only SSH, no public exposure

## Nodes

| Node | Hardware | Role |
|------|----------|------|
| Mac Studio | M1 Ultra, 128GB | Orchestrator — governance API, inference engine, search, gateway |
| Gemini | RTX 4070 Ti SUPER, 64GB | GPU compute — training, inference, video/image generation |
| Persius | RTX 4070 Ti SUPER, 64GB | GPU compute — training, inference, parallel workloads |
| iMac | Intel, macOS | Development, creative tools |
| MacBook Pro | macOS | Mobile development |
| Pi 1 | ARM, 16GB | Edge services, monitoring |
| Pi 2 | Raspberry Pi | Wake-on-LAN, lightweight services |

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                 Tailscale WireGuard Mesh             │
│                                                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐          │
│  │ Gemini   │  │ Persius  │  │ Mac Studio│          │
│  │ RTX 4070 │  │ RTX 4070 │  │ M1 Ultra  │          │
│  │ Ollama   │  │ Ollama   │  │ Ollama    │          │
│  │ ComfyUI  │  │ ComfyUI  │  │ Gov API   │          │
│  │ Video API│  │ Video API│  │ Gateway   │          │
│  └────┬─────┘  └────┬─────┘  │ Search    │          │
│       │              │        │ Inference │          │
│       └──────────────┴────────┴─────┬─────┘          │
│                                     │                │
│  ┌──────────┐  ┌──────────┐  ┌─────┴────┐          │
│  │  iMac    │  │ MacBook  │  │  Pi 1/2  │          │
│  │  Dev     │  │  Mobile  │  │  Edge    │          │
│  └──────────┘  └──────────┘  └──────────┘          │
└─────────────────────────────────────────────────────┘
```

## Key Services

| Service | Port | Node | Description |
|---------|------|------|-------------|
| Mesh Governance API | 8015 | Mac Studio | Jobs, nodes, memories, audit, instance chat |
| Integration Gateway | 8096 | Mac Studio | Unified routing to all backend services |
| Unified Model Gateway | 8092 | Mac Studio | Routes inference to Ollama across 3 nodes |
| Inference Engine | 8015 | Mac Studio | 146 models, 6 providers, key rotation |
| searchWeb | 8050 | Mac Studio | Multi-engine search + deep scraping |
| Ollama | 11434 | Gemini/Persius/Mac Studio | Local LLM inference |

## Stack

- **Languages**: Python, Swift, TypeScript
- **Inference**: Ollama, vLLM, FastAPI
- **Databases**: SQLite (WAL), PostgreSQL, ChromaDB
- **Networking**: Tailscale, SSH key-only auth
- **Orchestration**: launchd (macOS), systemd (Linux)
- **Security**: Honeypot services, threat intelligence DB, mesh-wide audit logging
- **CI/Coordination**: Mesh governance hooks on all 7 nodes, Claude Code instances with inter-node messaging

## Philosophy

Build the infrastructure. Own the compute. No cloud lock-in for the things that matter — inference, data, and orchestration stay on hardware you control.

---

*Private infrastructure. Not a product.*
