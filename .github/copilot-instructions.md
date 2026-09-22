# Repository Instructions

Inspect before editing. Never invent APIs or capabilities; verify Android API level, permissions, and actual device behavior. Prefer simple, reliable MVP implementations and preserve working code. Keep a deterministic heuristic fallback whenever local AI is unavailable. The LLM is a constrained planner only; policy validation and deterministic executors control device actions.

Build and test after every meaningful change, starting with the narrowest relevant check. Fix relevant errors before continuing and never claim success without verification. Update documentation when architecture, scope, risk, or behavior changes. Do not commit secrets or credentials. Prioritize the MVP, avoid unnecessary rewrites, respect Android platform limitations, and label unsupported operations with safe alternatives.

Autonomous workflow: inspect the owning code path, history, and nearby tests; state one local hypothesis and its cheapest disconfirming check; make the smallest focused edit; immediately run the narrowest relevant validation; repair and rerun on failure; then review the diff, update documentation, and report verified results and remaining risks. Continue through implementation and validation until the requested task is complete, asking only when a genuine product or environment decision blocks progress.
