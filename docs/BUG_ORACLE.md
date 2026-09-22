# Bug Oracle Design

## Purpose
The oracle detects semantic regressions in observed state. It reports what changed and whether that violates a declared expectation; it does not invent a root cause.

## State model
A StateSnapshot contains timestamp, target package/window, normalized screen identifier, accessible labels, declared semantic flags such as authenticated and form fields present, visible data markers, orientation, foreground/background signal, screen-state observation, connectivity, permission observations, and evidence references. Unknown fields remain unknown.

## Comparison rules
- Authentication regression: before authenticated=true and after authenticated=false or Login screen observed.
- Lost input: a declared field value/presence marker existed before and is absent after resume or transition.
- Unexpected navigation: observed normalized screen is outside the transition's allowed destination set.
- Duplicate result: a stable result identifier or count repeats unexpectedly after a repeated action.
- Target disappearance: target package/window disappears, exits, or becomes unavailable after an action; classify as crash-like only when the observation supports that wording.
- Unexpected transition: observed state does not match the declared expected transition and is not explained by an unsupported capability.

## Output
```json
{
  "classification": "STATE_REGRESSION",
  "summary": "Authentication state regression detected.",
  "expected": "Dashboard / authenticated",
  "observed": "Login / unauthenticated",
  "confidence": 1.0,
  "evidenceIds": ["..."],
  "rootCause": null
}
```

Confidence describes observation completeness, not causal certainty. A missing screenshot does not invalidate a node-based observation. If required fields are missing, return INCONCLUSIVE rather than guessing.

## Test strategy
Unit-test each rule with positive, negative, unknown, and noisy snapshots. Add an integration test for Login -> Dashboard -> lock/unlock -> Login. Assert that the output is a regression classification and never contains an unsupported causal claim.
