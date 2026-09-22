# Competitor Gap Analysis

## Accurate positioning
Appium, Maestro, Detox, Firebase Robo, and Firebase Test Lab can automate interactions, explore interfaces, run deterministic or generated flows, and in some cases assist with AI-based testing. EdgeCase Hunter must not claim those systems cannot test edge cases.

## Narrow differentiation
EdgeCase Hunter's proposed distinction is an adaptive edge-case decision loop: it represents current app/device state, combines state dimensions into candidate edge cases, tracks tested combinations and failures, chooses an unexplored candidate by estimated value, and updates memory after observing the result. The product is a focused hypothesis-selection layer for real-device state collisions, not a replacement for established automation infrastructure.

## Comparison
| Capability | Existing tools commonly provide | EdgeCase Hunter MVP focus |
|---|---|---|
| Scripted execution | Strong | Deterministic action engine |
| UI crawling/exploration | Available in several tools | Candidate edge-case generation informed by state and history |
| Device farm/scale | Strongest in Firebase ecosystem | One prepared iQOO device |
| Test authoring | Developer-defined flows and assertions | Small declared baseline plus adaptive next-edge choice |
| Semantic regression | Depends on assertions/AI features | Explicit state-regression oracle for declared demo state |
| Evidence | Logs, screenshots, reports vary | Reproduction sequence plus state/device evidence |
| Local planner | Not the universal default | Optional, feasibility-gated local model with heuristic fallback |

## Honest claims
Say: "EdgeCase Hunter focuses on deciding which unusual state combination to test next and preserving evidence." Do not say: "Other tools cannot explore" or "Other tools are only scripts." Position it as complementary: it can eventually generate candidates for, or sit beside, established execution and device-farm workflows.

## Validation needed
Interview or test against at least one representative workflow after the MVP. Measure whether the adaptive memory selects combinations a fixed flow would not have selected and whether the resulting evidence is more actionable for the demo user.
