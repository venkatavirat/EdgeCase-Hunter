# EdgeCase-Hunter
An on-device AI agent that will try to break Android apps by combining unexpected real-device states.

## Repository status

This repository currently contains the EdgeCase Hunter design and planning baseline for the iQOO Hackathon. Product implementation has not started. Android implementation begins during the official iQOO Hackathon build window, September 26-27, 2026.
### Problem

Developers test the expected user journey, but many mobile bugs appear only when real device states collide: rotation, background/foreground transitions, permission changes, interruptions, rapid interaction, connectivity changes, and sensor conditions.

Existing tools such as Appium, Maestro, Detox and Firebase Robo can automate mobile testing, but developers generally define the flows or exploration rules. EdgeCase Hunter focuses on discovering unexpected state combinations automatically.

### Solution

The planned EdgeCase Hunter MVP runs on the iQOO phone alongside the Android app under test. It will observe the app's UI and permitted device state, choose high-value unexplored edge cases, execute only validated actions, and record the exact sequence that produces a failure. A local model is a feasibility-gated option; a deterministic heuristic planner is always required.

Example:

**Login → rotate → background → resume → permission change → rotate**

→ **BUG FOUND**

**Reproduction:** rotate → background → resume → rotate
**Result:** authentication state lost
**Evidence:** screenshots + action sequence + device state

### Why the iQOO phone matters

The phone is not just the display. The MVP will use verified real-device conditions such as orientation, app lifecycle signals, permissions, connectivity, and screen state. Sensor availability and OEM behavior must be confirmed on the actual iQOO device before being claimed or used.

### AI

A local/open-source model may reason about the current state and choose the next high-value edge case if the device feasibility spike passes. Otherwise, the deterministic heuristic planner provides the same constrained interface. The deterministic test engine performs the actual actions and captures evidence.

### Office Kit

The phone is the test/execution environment while the laptop provides the development target and receives the generated reproduction report through a rehearsed phone-laptop transfer path such as USB/ADB or a local network endpoint.

### Demo

The planned demo gives EdgeCase Hunter a deliberately buggy Android app.

The agent explores it.

It discovers a failure that normal testing misses.

It automatically produces:

**BUG FOUND → exact reproduction steps → screenshots → device state → developer-ready report.**
