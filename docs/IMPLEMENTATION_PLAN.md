# 30-Hour Implementation Plan

The plan assumes two contributors where possible, but every milestone has a demonstrable exit condition. Time is elapsed hackathon time, not calendar promises.

| Time | Milestone | Exit condition |
|---|---|---|
| 0-2h | Project scaffold and device inventory | Android project builds; iQOO API/device facts recorded |
| 2-4h | Capability spike | Service enabled; observe target; test global actions, orientation, connectivity, screenshot support |
| 4-7h | Demo target | Login/Dashboard app installs, normal flow works, seeded resume regression is repeatable manually |
| 7-10h | Observation and evidence schema | StateSnapshot, action/evidence records serialize and are visible |
| 10-13h | Deterministic action engine | Allowlisted MVP actions execute or return explicit unsupported results |
| 13-16h | Memory and candidate generation | Coverage keys, history, and high-value unexplored candidates are unit-tested |
| 16-19h | Oracle | Regression, navigation, input, disappearance, duplicate, unsupported, and inconclusive outcomes tested |
| 19-21h | Planner abstraction | Heuristic path works end to end; local model spike decides whether optional integration continues |
| 21-24h | End-to-end loop | Observe -> choose -> validate -> execute -> observe -> oracle -> memory works on demo |
| 24-26h | Evidence report and laptop transfer | Report includes required fields and transfers through rehearsed path |
| 26-28h | Rehearsal and hardening | Three reproducible runs, recovery path, clean reset procedure, no false claims |
| 28-30h | Presentation freeze | Demo script, screenshots/video backup, architecture explanation, known limitations, and build artifact ready |

## Scope cut order
Cut local model integration first, then optional sensors/proximity, then broad target-app support. Do not cut deterministic execution, memory, oracle, evidence, or the seeded demo regression.

## Milestone 1
Create the Android scaffold and run a device/capability inventory on the actual iQOO. Begin with this PowerShell command from the repository root:

```powershell
adb devices; adb shell getprop ro.product.model; adb shell getprop ro.build.version.sdk
```

Then scaffold the smallest Kotlin Android app in the repository, connect the listed device, build/install it, and record the device model/API result in PROGRESS.md. No product feature is considered feasible until this check and the empty-app build succeed.
