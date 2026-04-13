# Architecture Research — IARIS

## Component Architecture

```
┌─────────────────────────────────────────────────────┐
│                    UI Layer                          │
│  ┌──────────────┐  ┌────────────────────────────┐   │
│  │  CLI (Textual)│  │  Web (React + Recharts)    │   │
│  └──────┬───────┘  └────────────┬───────────────┘   │
│         │                       │                    │
│         │    ┌──────────────┐   │                    │
│         └────┤  FastAPI API  ├──┘                    │
│              └──────┬───────┘                        │
│                     │ WebSocket + REST               │
├─────────────────────┼───────────────────────────────┤
│              ┌──────┴───────┐                        │
│              │  IARIS Core  │                        │
│              └──────┬───────┘                        │
│     ┌───────────────┼───────────────┐                │
│     │               │               │                │
│  ┌──┴──────┐  ┌─────┴─────┐  ┌─────┴──────┐        │
│  │Reasoning│  │  Learning  │  │Coordination│        │
│  │ Layer   │  │  Layer     │  │  Layer     │        │
│  └─────────┘  └─────┬─────┘  └─────┬──────┘        │
│                     │               │                │
│              ┌──────┴───────────────┴──────┐        │
│              │      Execution Layer        │        │
│              │  (Monitor + Score + Act)    │        │
│              └──────────┬─────────────────┘        │
│                         │                            │
├─────────────────────────┼───────────────────────────┤
│              ┌──────────┴─────────────────┐        │
│              │    OS Abstraction Layer     │        │
│              │  psutil (Win + Linux)       │        │
│              └────────────────────────────┘        │
│                                                      │
│  ┌────────────┐  ┌────────────┐  ┌───────────────┐  │
│  │  SQLite DB  │  │  Recipes   │  │  Dummy Procs  │  │
│  │  (persist)  │  │  (JSON)    │  │  (simulator)  │  │
│  └────────────┘  └────────────┘  └───────────────┘  │
└─────────────────────────────────────────────────────┘
```

## Data Flow

1. **Monitor** (Execution Layer) samples processes every 1s via psutil
2. **Classify** behavior patterns from raw metrics
3. **Score** allocation based on behavior + system state + signals
4. **Learn** via EWMA — update behavior signatures in knowledge base
5. **Coordinate** across workload groups — resolve conflicts
6. **Reason** — generate natural language explanations
7. **Display** — push updates to CLI and Web via WebSocket
8. **Act** — apply resource decisions (dummy in v1, real in v2)

## Build Order (Dependencies)

1. **OS Abstraction + Process Monitor** — Foundation everything depends on
2. **Behavior Classifier + Scoring Engine** — Core intelligence
3. **Learning System (EWMA + Knowledge Base)** — Needs monitor data
4. **System State Machine** — Needs metrics to determine state
5. **Workload Coordinator** — Groups processes, needs classifier
6. **Reasoning Engine** — Needs all above to explain
7. **Dummy Process Simulator** — Parallel with core, needed for testing
8. **FastAPI API Layer** — Exposes core to UIs
9. **CLI Dashboard** — Consumes API
10. **Web Dashboard** — Consumes API via WebSocket
11. **Demo Flow** — Integration of all components

## Key Boundaries

- **Core engine** is pure Python — no UI dependencies
- **API layer** wraps core — CLI and Web are equal consumers
- **Dummy processes** are separate from core — swap for real later
- **Storage** is abstracted — in-memory dict backed by SQLite
