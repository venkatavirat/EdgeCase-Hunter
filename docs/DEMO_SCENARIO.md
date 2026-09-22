# Demo Scenario

## Setup
- Laptop contains the EdgeCase Hunter build, demo APK, and report viewer/export path.
- iQOO is the real execution and observation device.
- AccessibilityService is enabled with only the required permissions.
- Network, orientation, and screen-state observations are shown as facts, not fabricated telemetry.
- The demo target is installed and reset to Login.

## Script
1. Show the target at Login and start a normal test.
2. Enter credentials and reach Dashboard.
3. Display: TESTING... Normal flow passed.
4. Display the observed baseline: Dashboard, authenticated, user data visible.
5. Show candidate edge cases and selected reason: LOCK_SCREEN -> UNLOCK because lifecycle interruption may expose state restoration issues.
6. Execute lock. Ask the operator to unlock if the device requires user assistance. Record any unsupported or assisted step.
7. Resume and observe Login.
8. Display: BUG FOUND, STATE REGRESSION.
9. Show expected Dashboard/authenticated versus observed Login/unauthenticated.
10. Reproduce twice more, showing 3/3.
11. Export evidence to the laptop: screenshots where available, timestamps, exact action sequence, state summaries, and device-state facts.

## Evidence language
Use "Authentication state regression detected." Do not claim an Activity lifecycle root cause unless the demo app itself provides direct evidence. Label the defect as intentionally seeded for the hackathon.

## Recovery
If local AI is unavailable, show the same experience with HeuristicPlanner and disclose "deterministic fallback." If lock/unlock is unsupported, use a capability-gated prepared-device workflow or demonstrate the oracle with a controlled lifecycle/resume trigger; never fake a successful device action.

## Office Kit workflow
Laptop -> demo APK and EdgeCase Hunter build -> iQOO. iQOO -> observation, planning, execution, evidence. iQOO -> generated report -> laptop. The transfer must be a working artifact path, such as USB/ADB or a local network endpoint validated during rehearsal, not a decorative diagram.
