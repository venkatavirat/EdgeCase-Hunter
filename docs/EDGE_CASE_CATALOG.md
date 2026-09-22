# Edge-Case Catalog

Each edge case is a named combination with required capabilities, preconditions, expected observation, and a coverage key. The MVP uses a small catalog so selection remains understandable.

| ID | Combination | Required capability | Value hypothesis |
|---|---|---|---|
| E01 | LOCK_SCREEN -> assisted UNLOCK -> RESUME | screen lock, foreground observation | lifecycle/authentication restoration |
| E02 | ROTATE portrait -> landscape -> portrait | orientation | state and form restoration |
| E03 | BACK -> RESUME | back, foreground observation | navigation/state preservation |
| E04 | OPEN_NOTIFICATIONS -> dismiss -> RESUME | notification global action | interruption recovery |
| E05 | HOME -> RESUME | home, foreground observation | background/foreground restoration |
| E06 | RAPID_TAP on declared target control | node/gesture execution | duplicate submission/debouncing |
| E07 | connectivity transition observation during flow | ConnectivityManager/device setup | offline/online state handling |
| E08 | permission-state observation before/after flow | observable permission state | authorization regression |

The planner may choose only candidates whose preconditions and capabilities are currently satisfied. Unsupported candidates remain visible as coverage gaps, not silently discarded. Sensor and proximity cases are optional additions after device inventory confirms availability and a useful target behavior.

## Coverage key
A coverage key is the normalized combination of target state, action sequence, and relevant device-state dimensions. The memory records attempted, completed, failed, unsupported, and inconclusive outcomes so the generator can prefer unexplored combinations.
