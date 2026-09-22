# MVP Specification

## MVP user flow
1. Select or launch the prepared demo target.
2. Observe and summarize the normal login/dashboard state.
3. Run the normal flow and record a passing baseline.
4. Generate candidate edge cases from available capabilities and history.
5. Select LOCK_SCREEN -> UNLOCK, using local planning if available or heuristic planning otherwise.
6. Validate each action against policy and device capability.
7. Execute through AccessibilityService and permitted Android APIs.
8. Observe the resulting state, compare it with the expected authenticated dashboard state, and classify a regression.
9. Capture screenshots, timestamps, action sequence, and device-state facts.
10. Repeat the reproduction three times and export a developer-readable report.

## Supported actions
- TAP
- LONG_PRESS
- SWIPE
- BACK
- HOME
- RECENTS
- LOCK_SCREEN
- OPEN_NOTIFICATIONS
- SCREENSHOT
- RAPID_TAP

Every action has a capability check, timeout, result status, and evidence entry. UNLOCK is user-assisted unless the prepared development device makes an allowed workflow possible; the UI must show that requirement.

## State observations
Required: foreground package/window, visible text and content descriptions where accessible, orientation, foreground/background signal, screen state when observable, connectivity state, permission-state observations available to the app/service, recent action, and timestamp. Optional: sensor snapshots, camera/microphone availability, proximity, and screenshots, only when supported and permitted.

## Planner contract
Input is a compact state summary plus exploration memory. Output is strict JSON:

```json
{
  "action": "LOCK_SCREEN",
  "reason": "A lifecycle interruption may expose state restoration bugs.",
  "priority": 0.91
}
```

The action must be from the allowlist, priority must be in [0,1], reason must be short, and malformed or unsafe output is rejected. Multi-step candidates are expanded and validated one action at a time.

## Oracle outcomes
- PASS: expected state remains consistent.
- STATE_REGRESSION: authenticated state, input, or other declared semantic state was lost.
- UNEXPECTED_NAVIGATION: observed screen differs from the declared expected route.
- DUPLICATE_RESULT: an operation produced an unexpected repeated result when an observable identifier exists.
- TARGET_DISAPPEARED: target package/window disappeared or crash-like behavior was observed.
- UNSUPPORTED: capability or permission prevented execution.
- INCONCLUSIVE: observations were insufficient.

## Demo target
A small prepared Android app has Login and Dashboard states. The intentional defect clears authentication on the lock/unlock resume path. The target exposes accessible labels for state observation. The bug is explicitly a demo fixture and must not be presented as a general Android failure.

## Acceptance tests
- Normal login baseline passes.
- LOCK_SCREEN is rejected if the service capability is absent and the UI explains why.
- Prepared-device lock/unlock path produces the declared regression.
- The oracle does not report a root cause it did not observe.
- The same evidence schema works for local and heuristic planning.
