# Production Studio Implementation Rules

Mandatory implementation constraints for every Studio project and coding agent.
Apply them before choosing or writing a mechanism.

A project may record a narrow durable exception in its standing instructions or
design when its requirements justify one. `D-###` work items own neither rules
nor exceptions; `INV-`, `KP-`, and retrospectives may hold evidence, not the rule.

## Proof and implementation speed

Production Studio Fast Track governs all coding work: each change must leave the
next work both better engineered and faster to build.

For Negligible and Small work, prove the change by the cheapest credible means
first: existing checks that own it, normal validation, direct inspection of the
changed source and control flow, then broader existing checks only as needed.
Probes, harnesses, mutation tests, and instrumentation are escalation, not the
default, and count as cost even when deleted. Before adding one, name the important fact still
unproved, why cheaper proof cannot establish it, and why the added cost is
justified.

If proof or debugging becomes disproportionate to the change, or proof machinery
itself needs substantial debugging, stop and simplify before expanding it. Do
not re-prove unchanged neighboring invariants with reliable owners. Correct
another document only when this change makes a current statement there false or
incomplete; never by term-matching audit.

## Waits and synchronization

Every operational wait, poll, retry, or synchronization needs a real success
condition and a deliberate non-success exit; none may trap indefinitely. Prefer
observable readiness, progress, and failure to elapsed time. Where the program
can observe that success will not occur without another action, detect that
state and stop automatically. Cancellation is useful backup user control, and
never by itself corrects a wait that can otherwise stay forever in a failed or
stalled state the program could reasonably recognize. Consider a narrowly
justified failsafe bound only where no credible observable failure or progress
signal exists; this is not a blanket timeout policy. Do not use `Sleep` or a
fixed delay for readiness when a credible observable signal exists; use one only
when the delay itself is required or no credible observable replacement exists.
Where legitimate work and a stall would otherwise look alike for a long time,
expose meaningful waiting, progress, or failure status where practical.

Long-lived event loops, servers, watchers, and observers are not operational
waits.

## Correct the owner, not the symptom

Fix a defect at its owner across the defect class, not only at the visible
instance, and correct, prevent, or reliably detect the condition that creates
the failure before adding recovery from its consequences. Inspect equivalent and
sibling paths and deterministic downstream behavior. A retry, fallback, timeout,
cancellation path, escape hatch, restart, warning, or manual workaround does not
count as fixing the defect when the underlying failure can reasonably be
prevented or recognized at its source. Recovery may be secondary protection
after the fundamental correction, or the deliberately chosen result only when the
underlying defect is explicitly left in place because correcting it is
impossible, unsupported, or not worth its cost. Do not convert `smallest
solution` into `smallest patch after failure`: prefer the smallest solution that
removes, prevents, or reliably detects the failure itself. One successful local
patch is not completion evidence.

## Reuse existing behavior; add new behavior as a leaf

Before adding implementation or debugging machinery, identify each needed
operation's owner, target, timing, status (designed, implemented, or deliberately
unsettled), and regression coverage. Build a parallel mechanism only after
proving the existing one cannot meet the need. If the difference is caller
state, correct the caller and keep the shared mechanism. Edit a shared helper for
one caller only when a leaf provably cannot work.

## Working or removed

Prove the path or remove it and let the code assume correct conditions. Never
retain an unverified fallback; Git preserves removed code.

## Durable files contain no one-run state

Do not put run IDs, PIDs, tokens, transfer markers, timestamps, or other one-run
values in standing instruction or design files.

## Enumerate before filtering

To locate a file, window, element, process, or record, enumerate what exists
before narrowing. Do not guess identity before seeing the candidates.

## Trace values through the whole path

Before declaring a value change complete, follow it through every transform,
store, render, control size, and layout step that can affect the result.

## Comments describe the current system

Write comments for a future reader: current behavior, plus only the reason or
history needed to understand it. Git owns obsolete history.
