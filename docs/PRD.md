# Product Requirements Document

## Product
EdgeCase Hunter is an Android developer tool that chooses which unusual combination of real app and device states to test next. Its value is adaptive decision-making: observe the current state, generate candidate edge cases, choose the most valuable unexplored candidate, execute it through a deterministic capability-gated engine, compare the result with the expected state, and record reproducible evidence.

Tagline: "Developers test what they expect. EdgeCase Hunter tests what they didn't think of."

## Users and problem
The primary user is an Android developer or QA engineer who can describe a normal flow but cannot manually cover the combinatorial interactions among lifecycle, orientation, interruption, permissions, connectivity, and rapid input. Existing tools such as Appium, Maestro, Detox, Firebase Robo, and Firebase Test Lab provide real automation, crawling, and test execution. EdgeCase Hunter complements them by selecting high-value state combinations and explaining the evidence for a regression.

## Hackathon outcome
A live iQOO demonstration starts with a normal login flow, then EdgeCase Hunter selects LOCK_SCREEN -> assisted UNLOCK, executes the supported portion, detects that the deliberately buggy app returned to Login, and produces a report with 3/3 reproduction evidence.

## Goals
- Demonstrate adaptive edge-case selection, not random action spam.
- Make the iQOO phone the real observation and execution environment.
- Detect semantic state regressions using observed evidence.
- Produce a deterministic reproduction sequence and report.
- Operate with a local model when feasible and always operate with a heuristic fallback.

## Non-goals
Universal mobile testing, autonomous root-cause analysis, unrestricted device control, guaranteed support for every Android app, cloud-scale test orchestration, and a production-grade local LLM runtime are outside the 30-hour MVP.

## Success criteria
- A fresh build can run the demo flow on the target iQOO device.
- The planner returns strict, validated action JSON or a deterministic fallback action.
- At least the MVP actions execute or are explicitly reported unsupported.
- The demo bug is detected as authentication/state regression, without invented root cause.
- A report contains action sequence, timestamps, before/after summaries, device-state observations, and screenshots where permitted.
- A second run reproduces the same bug at least 3 out of 3 times in the prepared demo setup.

## Product principles
1. AI proposes; policy validates; deterministic code executes.
2. Observed state is evidence; explanations remain bounded by evidence.
3. Exploration memory makes the next choice more valuable than the last.
4. Capability failure is a visible result, never a silent success.
5. The fallback path is a first-class demo path.
