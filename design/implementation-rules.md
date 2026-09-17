# Production Studio Implementation Rules

Mandatory for every Studio project and coding agent before claiming a gap or proposing, choosing, writing, implementing, or debugging a mechanism. A project may record a narrow durable exception in standing instructions or design when its requirements justify one. `D-###` owns neither rules nor exceptions; `INV-`, `KP-`, and retrospectives hold evidence only.

## Proof and implementation speed

Production Studio Fast Track governs all coding work: each change must leave the next work better engineered and faster to build.

For Negligible/Small work, use the cheapest credible proof: owning checks, normal validation, changed-source/control-flow inspection, then broader existing checks only as needed. Probes, harnesses, mutation tests, and instrumentation are escalation and count as cost even when deleted. Before adding one, name the unproved fact, why cheaper proof cannot establish it, and why the cost is justified. Use applicable ordinary non-executing validation before temporary executable proof/debugging.

If proof/debugging becomes disproportionate or its machinery needs substantial debugging, stop and reassess before expanding; simplify only when reassessment shows unnecessary cost. Do not re-prove unchanged neighboring invariants with reliable owners. Correct another document only when this change makes a current statement false or incomplete, never by term-matching audit.

## Waits and synchronization

Every operational wait, poll, retry, or synchronization needs a real success condition and deliberate non-success exit; none may trap indefinitely. Prefer observable readiness/progress/failure to elapsed time. When the program can observe that success will not occur without another action, detect that state and stop automatically. Cancellation is backup control, not correction for a detectable stall. Use a narrowly justified failsafe bound only where no credible observable failure/progress signal exists; this is not a blanket timeout policy. Do not use `Sleep` or fixed delay for readiness when a credible observable signal exists; use one only when the delay itself is required or no credible observable replacement exists. Where legitimate work and a stall would otherwise look alike for long periods, expose meaningful waiting/progress/failure status where practical. Long-lived loops, servers, watchers, and observers are not operational waits.

## Correct the owner, not the symptom

Fix a defect at its owner across the defect class; prevent or reliably detect its cause before recovery. Inspect equivalent/sibling paths and deterministic downstream behavior. Retry, fallback, timeout, cancellation, escape, restart, warning, or manual workaround is not the fix when source correction/detection is reasonable. Recovery may be secondary, or the deliberate result only when root correction is impossible, unsupported, or not worth its cost. Prefer the smallest solution that removes, prevents, or reliably detects the failure, not the smallest patch after it. One local success is not completion evidence.

## Do not treat an intentional workflow result as a failure

When a workflow deliberately stops, closes, reloads, releases a lock, clears temporary state, disconnects, or otherwise causes a state as part of its intended transition, the result itself is not a defect. Do not diagnose it as though something unexpectedly broke, and do not build recovery merely to undo what the workflow intentionally did.

Instead, verify that the intended action actually succeeded and that the workflow can continue from the intended resulting state. If a process was supposed to stop but is still running, a lock was supposed to be released but remains held, a reload never becomes ready, or the workflow fails to reach its required destination, that is a real failure.

Use facts the workflow already established instead of creating duplicate state or re-detecting what the workflow already knows. Do not add crash classification, recovery flags, self-healing, or other detection/recovery machinery solely because an intentional transition resembles a failure state. Legitimate prerequisite checks, refusals, bounded retries, failure handling, and future-compatibility safeguards remain allowed where they independently earn their cost.

This applies both to Production Studio tooling and to workflows inside the products we build.

## Establish the need; reuse existing behavior

Before calling something missing or needed, or offering a mechanism, inspect only the relevant current behavior and closest existing owner or solution enough to establish that a user need remains. Include accepted human prerequisites, refusals, guards, unsupported cases, and simple manual correction. If no agreement settles the case, present the choice among a simple refusal, user prerequisite, manual correction, or machinery rather than assuming machinery. If required reading is not permitted, call the point unestablished, not missing. If no need remains, state the actual mismatch instead of inventing a capability gap.

If a need remains, prefer direct reuse, then a small refactor for reuse, then its proven mechanism with only the new leaf; a partial mismatch is not a reason to start over.

Before adding implementation/debugging machinery, identify each needed operation's owner, target, timing, status (designed, implemented, or deliberately unsettled), and regression coverage. Build a parallel mechanism only after proving the existing one cannot meet the need. If the difference is caller state, correct the caller and keep the shared mechanism. Edit a shared helper for one caller only when a leaf provably cannot work.

## Working or removed

Prove the path or remove it and let code assume correct conditions. Never retain an unverified fallback; Git preserves removed code.

## Durable files contain no one-run state

Do not put run IDs, PIDs, tokens, transfer markers, timestamps, or other one-run values in standing instruction or design files.

## Line endings belong to the repository

Decide line endings once in repository policy, normally `.gitattributes`, not per-file exceptions. Byte-for-byte checks normalize endings before comparing/hashing so natural editor, agent, or shell endings do not break them.

## Enumerate before filtering

Enumerate candidates before narrowing a file, window, element, process, or record; do not guess identity first. A destructive debugging or cleanup action against a live process or resource acts only on exact identities established before it runs, never on a name, path, or pattern that could match unrelated live state.

## Trace values through the whole path

Before declaring a value change complete, follow every transform, store, render, control size, and layout step that can affect it.

## Comments describe the current system

Comments state current behavior plus only reason/history needed to understand it. Git owns obsolete history.

## User-visible identifiers name their type

New user-visible identifiers begin with type: `ERR-` failure, `NOTICE-` information, `WARN-` only for a genuinely distinct warning. Subsystem and number follow unchanged. This governs new identifiers only and is not authority to rename existing ones, which records, search terms, and written logs already name.
