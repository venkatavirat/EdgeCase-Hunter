# Technical Decisions

## ADR-001: Native Kotlin Android
Status: accepted for planning. Native Kotlin matches the target platform, accessibility APIs, device sensors, and hackathon delivery constraints.

## ADR-002: Planner/executor separation
Status: accepted. The planner returns a constrained proposal. Policy validation and deterministic executors own permissions, capabilities, timing, and device actions. This bounds model failure and makes tests repeatable.

## ADR-003: LocalModelProvider abstraction
Status: accepted. The interface exposes state-summary input and strict planner output. Implementations are LocalModelPlanner and HeuristicPlanner. Runtime/model integration is conditional on the feasibility spike.

## ADR-004: Accessibility-first external observation
Status: accepted for MVP, conditional on user-enabled service and target semantics. The target demo app will expose accessible state labels. Instrumentation is preferred for the demo app when it gives stronger ground truth.

## ADR-005: Declared semantic state
Status: accepted. The oracle compares declared/observed facts such as authenticated and screen identity rather than attempting universal visual understanding.

## Open decisions
- Exact Android API/minSdk/targetSdk after project scaffold and target-device inventory.
- Whether LiteRT-LM/Gemma meets latency, memory, and JSON reliability gates.
- Screenshot transport and laptop report transfer method.
- Whether iQOO OEM behavior supports the required global actions reliably.

## Decision log rule
Every open decision must record evidence, device/API context, date, and consequence in PROGRESS.md before it becomes an implementation assumption.

## Design consistency review
Reviewed against the 30-hour constraint. The local model is optional and cannot block the heuristic path; unlock is assisted or capability-gated; screenshots and sensors are optional evidence; semantic oracle claims are limited to observed state; and competitor positioning is complementary. Universal target-app support, broad sensor exploration, cloud scale, causal diagnosis, and unverified LiteRT-LM integration were removed from the MVP commitment.
