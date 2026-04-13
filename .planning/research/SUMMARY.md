# Research Summary — IARIS

## Key Findings

### Stack
- **Python 3.11+** with **psutil** for cross-platform process monitoring
- **Rich/Textual** for CLI dashboard (async-native, beautiful TUI)
- **FastAPI** with **WebSocket** for real-time API layer
- **React 18 + Recharts + Vite** for web dashboard
- **SQLite** for persistence, in-memory dicts for hot path

### Table Stakes
- Process monitoring (CPU, memory, I/O) via psutil
- Behavior classification (CPU hog, latency-sensitive, bursty, blocking)
- Resource allocation scoring with configurable formulas
- System state detection (Stable/Pressure/Critical)
- Decision audit trail and logging
- Real-time metric display (CLI + Web)

### Differentiators
- **EWMA-based behavioral learning** — adapts over time, not static rules
- **Behavior signatures** — hash-based process fingerprinting
- **Natural language reasoning** — explains every decision transparently
- **Workload abstraction** — groups related processes for coordinated management
- **Cold-start recipes** — JSON hints for immediate initial behavior

### Watch Out For
1. **Monitoring overhead** — Use `process_iter()`, 1s sampling, batch collection
2. **Race conditions** — Always handle `NoSuchProcess`/`AccessDenied` exceptions
3. **EWMA cold start** — Use recipes + warmup period with higher alpha
4. **Cross-platform differences** — Abstract OS-specific calls from day 1
5. **WebSocket memory leaks** — Connection manager with heartbeat + pruning
6. **UI overload** — Throttle updates, paginate, batch state changes

### Build Order
1. OS Abstraction + Process Monitor (foundation)
2. Dummy Process Simulator (parallel, needed for testing)
3. Behavior Classifier + Scoring Engine
4. Learning System (EWMA + Knowledge Base)
5. System State Machine + Workload Coordinator
6. Reasoning Engine
7. FastAPI API Layer
8. CLI Dashboard (Textual)
9. Web Dashboard (React)
10. Demo Flow Integration
