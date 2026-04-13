# Pitfalls Research — IARIS

## Critical Pitfalls

### 1. Monitoring Overhead Kills Performance
**Warning signs:** CPU usage from IARIS itself exceeds 1%, system becomes sluggish
**Prevention:** 
- Use `psutil.process_iter()` not manual PID iteration
- 1-second sampling interval (not sub-second)
- Batch metric collection, don't query per-process sequentially
- Cache process objects, re-query only changed PIDs
**Phase:** Phase 1 (Monitor Foundation)

### 2. Race Conditions in Process Monitoring
**Warning signs:** `NoSuchProcess`, `AccessDenied`, `ZombieProcess` exceptions
**Prevention:**
- Always wrap psutil calls in try/except for these three exceptions
- Never assume a PID is still valid between calls
- Use `psutil.process_iter(attrs=[...])` with specific attributes
**Phase:** Phase 1 (Monitor Foundation)

### 3. EWMA Cold Start Problem
**Warning signs:** System makes poor decisions for first few minutes
**Prevention:**
- JSON recipe files provide initial behavior hints
- Set minimum observation window before IARIS starts acting
- Use higher alpha (0.5) during warmup, lower (0.3) at steady state
**Phase:** Phase 3 (Learning System)

### 4. WebSocket Memory Leaks
**Warning signs:** Server memory grows unbounded, connection count never decreases
**Prevention:**
- Implement connection manager with heartbeat ping/pong
- Set maximum connections limit
- Prune zombie connections on timeout
- Cap message queue per client
**Phase:** Phase 5 (API Layer)

### 5. Cross-Platform Behavior Differences
**Warning signs:** System works on Linux but fails on Windows (or vice versa)
**Prevention:**
- Abstract all OS-specific calls behind platform detection
- Test on both platforms from day 1
- psutil API differences: cpu_affinity not on macOS, ionice Linux-only
- Process priority APIs differ between Windows and Linux
**Phase:** Phase 1 (from the start)

### 6. Dummy Process Simulation Too Simple
**Warning signs:** IARIS looks great on dummies but fails on real processes
**Prevention:**
- Dummy processes should exhibit realistic patterns (bursts, I/O waits, memory growth)
- Include multiple behavior types, not just CPU hogs
- Add randomness and variation to dummy patterns
**Phase:** Phase 2 (Dummy Processes)

### 7. UI Overloading Browser/Terminal
**Warning signs:** Dashboard becomes sluggish with many processes
**Prevention:**
- Throttle UI updates (max 1 update/second to frontend)
- Paginate process lists, don't render all at once
- Use virtual scrolling for large lists
- Batch state updates on frontend
**Phase:** Phase 6-7 (Dashboards)
