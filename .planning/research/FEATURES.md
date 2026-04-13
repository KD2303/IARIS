# Features Research — IARIS

## Table Stakes (Must Have)
These are expected in any resource intelligence / process scheduling system:

| Feature | Complexity | Dependencies |
|---------|-----------|--------------|
| Process monitoring (CPU, memory, I/O) | Low | psutil |
| Process behavior classification | Medium | Monitoring data |
| Resource allocation scoring | Medium | Behavior classification |
| System state detection (normal/pressure/critical) | Low | Monitoring data |
| Decision logging / audit trail | Low | Storage layer |
| Configuration via files | Low | JSON parsing |
| Real-time metric display | Medium | Monitoring + UI |

## Differentiators (Competitive Advantage)
These set IARIS apart from traditional schedulers:

| Feature | Complexity | Dependencies |
|---------|-----------|--------------|
| EWMA-based behavioral learning | Medium | Monitoring over time |
| Behavior signature generation | Medium | Learning system |
| Intent inference from behavior patterns | High | Learning + signatures |
| Natural language reasoning/explanations | Medium | Decision engine |
| Workload abstraction (group processes) | Medium | Process monitoring |
| Temporal pattern detection | High | Learning over sessions |
| Cold-start recipes (JSON hints) | Low | Config system |
| Predictive resource pre-allocation | High | Temporal intelligence |

## Anti-Features (Deliberately NOT Building)
| Anti-Feature | Why Not |
|-------------|---------|
| Real-time kernel module | Too risky for hackathon, cross-platform impossible |
| ML model training pipeline | EWMA is sufficient, no GPU dependency |
| Container orchestration | Out of scope for v1 |
| Network traffic shaping | Too OS-specific |
| GUI desktop app | Web + CLI covers all demo needs |
