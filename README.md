# EdgeCase-Hunter
An on-device AI agent that tries to break Android apps by combining unexpected real-device states.
### Problem

Developers test the expected user journey, but many mobile bugs appear only when real device states collide: rotation, background/foreground transitions, permission changes, interruptions, rapid interaction, connectivity changes, and sensor conditions.

Existing tools such as Appium, Maestro, Detox and Firebase Robo can automate mobile testing, but developers generally define the flows or exploration rules. EdgeCase Hunter focuses on discovering unexpected state combinations automatically.

### Solution

EdgeCase Hunter runs on the iQOO phone alongside the Android app under test. An on-device AI agent observes the app's UI and current device state, chooses high-risk edge cases to explore, executes them, and records the exact sequence that produces a failure.

Example:

**Login → rotate → background → resume → permission change → rotate**

→ **BUG FOUND**

**Reproduction:** rotate → background → resume → rotate
**Result:** authentication state lost
**Evidence:** screenshots + action sequence + device state

### Why the iQOO phone matters

The phone is not just the display. EdgeCase Hunter uses real device conditions including orientation/motion, app lifecycle, permissions, connectivity and other device state. The iQOO hardware provides the actual environment in which mobile bugs occur.

### AI

A local/open-source model runs on-device to reason about the current state and choose the next high-value edge case. The deterministic test engine performs the actual actions and captures evidence.

### Office Kit

The phone is the test/execution environment while the laptop provides the development target and receives the generated reproduction report through the phone–laptop bridge.

### Demo

Give EdgeCase Hunter a deliberately buggy Android app.

The agent explores it.

It discovers a failure that normal testing misses.

It automatically produces:

**BUG FOUND → exact reproduction steps → screenshots → device state → developer-ready report.**
