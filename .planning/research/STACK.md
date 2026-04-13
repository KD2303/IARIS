# Stack Research — IARIS

## Recommended Stack (2025)

### Core Engine
| Component | Choice | Version | Confidence | Rationale |
|-----------|--------|---------|------------|-----------|
| Language | Python | 3.11+ | ★★★★★ | Best psutil support, rapid prototyping, cross-platform |
| Process Monitoring | psutil | 5.9+ | ★★★★★ | Industry standard, cross-platform (Win+Linux), mature API |
| Async Runtime | asyncio | stdlib | ★★★★★ | Native to Python, required by Textual and FastAPI |

### Learning & Storage
| Component | Choice | Version | Confidence | Rationale |
|-----------|--------|---------|------------|-----------|
| Knowledge Base | SQLite | stdlib | ★★★★★ | Zero-config, file-based, perfect for hackathon |
| In-Memory Cache | dict + dataclasses | stdlib | ★★★★★ | Hot data path, no external dependency |
| Serialization | JSON | stdlib | ★★★★★ | Human-readable recipes, config files |

### CLI Dashboard
| Component | Choice | Version | Confidence | Rationale |
|-----------|--------|---------|------------|-----------|
| TUI Framework | Rich + Textual | 0.50+ | ★★★★☆ | Best Python TUI framework, async-native, beautiful output |
| CLI Args | typer | 0.9+ | ★★★★☆ | Clean CLI interface, built on Click |

### Web Dashboard
| Component | Choice | Version | Confidence | Rationale |
|-----------|--------|---------|------------|-----------|
| Backend API | FastAPI | 0.100+ | ★★★★★ | Async, WebSocket support, auto-docs, Python-native |
| Real-time Comm | WebSocket | native | ★★★★★ | Bidirectional, low-latency updates |
| Frontend | React 18 | 18.2+ | ★★★★★ | Rich ecosystem, good for real-time data viz |
| Charts | Recharts | 2.x | ★★★★☆ | React-native charting, great for time-series |
| Build Tool | Vite | 5.x | ★★★★★ | Fast dev server, modern bundling |

### What NOT to Use
- **Django** — Too heavy for a real-time monitoring system
- **Flask** — No native async/WebSocket support
- **Kubernetes/Docker** — Adds complexity without value for v1 dummy processes
- **Prometheus/Grafana** — Overkill; we need custom behavior analysis, not generic metrics
- **curses** — Low-level; Rich/Textual provides much better abstractions
