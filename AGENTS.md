# EdgeCase Hunter Agent Instructions

## Before editing
- Inspect the relevant files, history, and nearby tests before changing anything.
- State the local hypothesis and the cheapest check that can disconfirm it.
- Prefer the smallest change that tests the hypothesis.

## Autonomous implementation workflow
- Identify the owning code path and acceptance behavior before editing.
- Make the smallest focused change that tests the hypothesis.
- Immediately run the narrowest relevant build, test, lint, or type check after the edit.
- If validation fails, repair the same slice and rerun that check before expanding scope.
- Review the diff, update affected documentation, and report verified results and remaining risks.
- Continue through implementation, validation, and documentation until the requested task is complete; ask only when a genuine product or environment decision is blocking progress.

## Engineering rules
- Target native Android/Kotlin and preserve working code.
- Never invent Android, accessibility, sensor, AI, or device APIs. Verify API level, permission, and device behavior before relying on them.
- Prefer simple, reliable implementations over broad platform abstractions.
- Keep the deterministic heuristic fallback working whenever local AI is unavailable.
- Treat the LLM as a constrained planner: it proposes validated actions; it never receives unrestricted shell or device access.
- Mark restricted capabilities unsupported and provide a safe alternative.
- Prioritize the MVP and avoid unnecessary rewrites.
- Do not commit secrets, tokens, credentials, or device data.

## Validation
- Build and test after changes. Run the narrowest relevant check first, then widen only when useful.
- Fix relevant errors before continuing.
- Never claim success without command output or another explicit verification.
- Add focused tests for planner, policy validation, memory, oracle, and report serialization.
- Update the applicable documentation when behavior, scope, risk, or architecture changes.

## Product constraints
- The MVP must prefer unexplored, high-value edge-case combinations rather than random action spam.
- Evidence must distinguish observed facts from inferred explanations.
- Do not claim competitors lack capabilities they demonstrably have.
- Keep the iQOO device central to execution and evidence, not decorative.
