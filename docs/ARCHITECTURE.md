# Architecture

## System boundary
EdgeCase Hunter runs on the iQOO phone beside the target app. The target app may be the seeded demo or a prepared developer app. The laptop supplies APKs/builds and receives an exported report; it is not required for the core exploration loop.

## Components
- StateObserver: collects accessibility/window/package observations plus permitted device state and produces normalized StateSnapshot values.
- ExplorationMemory: stores snapshots, actions, candidate coverage keys, outcomes, failures, and interesting transitions.
- EdgeCoverageTracker: normalizes combinations and reports attempted, completed, unsupported, failed, and unexplored edges.
- CandidateEdgeCaseGenerator: creates bounded candidates from the catalog, current state, capabilities, and memory; scores novelty, risk/value, observability, and cost.
- LocalModelProvider: common planner interface with LocalModelPlanner and HeuristicPlanner implementations.
- PolicyValidator: allowlist, schema, capability, precondition, timeout, and rate-limit checks.
- DeterministicActionEngine: executes validated actions using accessibility/global actions, gestures, Android observations, or explicit assisted steps.
- BugOracle: compares expected and observed semantic state and emits bounded classifications.
- EvidenceRecorder: persists timestamps, sequence, snapshots, device facts, screenshots, outcome, and report metadata.
- ReportExporter: creates a human-readable report and transfers it through a rehearsed laptop path.
- Demo target: small app with stable accessible state labels and a seeded lock/resume authentication regression.

## Control flow
```text
StateObserver -> StateSnapshot
StateSnapshot + ExplorationMemory -> CandidateEdgeCaseGenerator
Candidate + summary + memory -> LocalModelProvider
Proposal -> PolicyValidator -> DeterministicActionEngine
Action result -> StateObserver -> BugOracle
Oracle result -> ExplorationMemory + EvidenceRecorder -> ReportExporter
```

## Planner contract
The planner receives a bounded serialized summary, never a shell, unrestricted accessibility command channel, credentials, or arbitrary code execution authority. It returns action, reason, and priority. The validator rejects unknown actions, invalid ranges, malformed JSON, missing preconditions, unsupported capabilities, and unsafe rates.

## Memory model
```text
ExplorationMemory
  runId
  currentState: StateSnapshot
  previousStates: StateSnapshot[]
  actionHistory: ActionRecord[]
  coverage: EdgeCoverageRecord[]
  failures: Finding[]
  interestingTransitions: Transition[]
```

An edge key includes target state identifier, normalized action sequence, and relevant device-state dimensions. A bounded ring/history or persisted JSON/Room store is sufficient for the MVP; choose the simplest implementation after scaffold.

## Reliability boundaries
Unknown observations remain unknown. Unsupported actions produce evidence and coverage gaps. The heuristic planner is always available. The oracle never asserts causality without direct evidence. The demo app may use instrumentation for ground truth while the external service demonstrates the same observable workflow.
