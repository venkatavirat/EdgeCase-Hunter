# Technical Feasibility

## Baseline
The repository currently contains no Android project, Gradle wrapper, Kotlin code, device service, or tests. Feasibility is therefore a design assessment until a minimal Android spike runs on the actual iQOO phone.

## Feasible MVP building blocks
- Kotlin Android app and a deliberately buggy demo target are standard.
- AccessibilityService can observe accessibility windows/nodes when the user enables the service and the target exposes useful semantics.
- Accessibility global actions provide supported paths for Back, Home, Recents, and notification shade on compatible API levels.
- AccessibilityService can request a screenshot on API levels that support the relevant API and device policy; this must be verified on the target.
- Orientation can be observed through configuration/display APIs and sensor APIs where permitted.
- Connectivity state can be observed through ConnectivityManager callbacks and active-network capabilities, with permission/API caveats.
- Camera and microphone permission state can be observed for the relevant app only where Android exposes it; hardware privacy indicators and another app's internal state are not universally readable.
- Lifecycle and foreground/background can be approximated from accessibility window/package events and the target's own instrumentation; an external service cannot promise perfect lifecycle semantics.

## Restricted or conditional capabilities
- Unlocking a secure device is not a normal unrestricted app capability. The MVP uses user-assisted unlock or a prepared development-device workflow and records that fact.
- Screen lock through a global action requires service capability, API support, and user-enabled accessibility service; it is not silently guaranteed.
- Arbitrary taps and gestures require node coordinates/gesture support and can fail due to overlays, secure windows, or target behavior.
- Notifications, lock screen, screenshots, and recents may be affected by OEM policies, secure surfaces, API level, and accessibility settings.
- Proximity availability varies by device and sensor inventory. It is optional and must be reported as unavailable when absent.
- Reading another app's private data, logs, or root cause is out of scope.

## Local AI feasibility gate
LiteRT-LM and a suitable Gemma-family model are candidates, not assumptions. Before integrating, run a spike on the exact device and Android build to verify artifact availability, ABI, RAM/storage, startup latency, token latency, thermal behavior, and output reliability. If the spike fails or threatens the demo, use HeuristicPlanner behind the same LocalModelProvider interface. Do not package an unverified runtime in the MVP.

## Required spike measurements
Record device model, Android/API level, available RAM/storage, model size, load time, first-token and total latency, temperature/throttling symptoms, malformed JSON rate across a small fixed corpus, and battery impact. The result belongs in TECH_DECISIONS.md and PROGRESS.md.

## Feasibility conclusion
The deterministic observation/execution/oracle demo is feasible in 30 hours if scope stays narrow. Full local generation, reliable cross-app semantic understanding, secure unlock automation, and broad OEM compatibility are not feasibility assumptions; they are gates or explicit exclusions.
