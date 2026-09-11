# lingshu-gpu-scheduler

Distributed scheduler with ControllerManager-style election.

## Core modules

- **ResourceViewManager** — `ConcurrentHashMap<workerId, GpuWorkerNode>` + 15s heartbeat timeout + MySQL persistence
- **GpuLoadBalancer** — `score = mem×0.5 + util×0.3 + queue×0.2`; same-node affinity (Soft Hint)
- **TaskStateMachine** — `PENDING → QUEUED → ASSIGNED → RUNNING → SUCCESS/FAILED/TIMEOUT/CANCELLED/ORPHAN`
- **ControllerManager** — multi-round voting + `force=true` anti-split-brain + `RESET_CONTROLLER` (reused from ruyuan-cloud-server)

## MVP scope (STORY-2-2 / STORY-2-3)

- Single instance (no election yet)
- 3 worker node limit
- MySQL state persistence (no Redis Cluster)

## v0.5

Multi-replica + ControllerManager activation, priority preemption.
