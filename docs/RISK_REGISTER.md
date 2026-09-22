# Risk Register

| Risk | Likelihood | Impact | Mitigation / trigger |
|---|---:|---:|---|
| Accessibility actions differ on iQOO/OEM build | High | High | Spike Back/Home/Recents/lock/screenshot first; show unsupported status and use prepared fallback |
| Secure unlock cannot be automated | High | High | User-assisted unlock or allowed prepared development workflow; never fake success |
| Local model cannot run within RAM/latency budget | High | Medium | Validate exact device early; ship deterministic heuristic planner |
| Accessibility tree lacks useful semantic labels | Medium | High | Instrument demo target, add stable content descriptions, classify unknowns |
| Screenshot API/policy restrictions | Medium | Medium | Treat screenshots as optional evidence; preserve node/state/timestamp evidence |
| Connectivity/sensor signals are noisy or unavailable | Medium | Medium | Record capability and unknown state; do not infer unavailable data |
| Oracle false positives from weak state summaries | Medium | High | Declared demo state, confidence, INCONCLUSIVE outcome, focused tests |
| 30-hour scope expands into a platform | High | High | Freeze MVP catalog and acceptance tests; defer listed non-goals |
| Demo setup or transfer fails | Medium | High | Rehearse reset, APK install, service enablement, and report transfer; keep local report export |
| Device overheats or battery drops | Medium | Medium | Short runs, monitor thermal/battery facts, disable unneeded model path |
| Credentials or screenshots leak | Low | High | Synthetic demo data, no secrets, local evidence retention and cleanup |
| Model output is malformed or unsafe | Medium | Medium | Strict schema parsing, allowlist, bounds, timeout, heuristic fallback |

## Stop conditions
If a high-impact risk has no verified mitigation by the end of the first device spike, remove that capability from the live demo and update MVP_SPEC.md, DEMO_SCENARIO.md, and PROGRESS.md.
