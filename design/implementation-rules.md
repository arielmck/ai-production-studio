# Production Studio Implementation Rules

Mandatory for every Studio project and coding agent before claiming a gap or proposing, choosing, writing, implementing, or debugging a mechanism. A project may record a narrow durable exception in standing instructions or design when its requirements justify one. `D-###` owns neither rules nor exceptions; `INV-`, `KP-`, and retrospectives hold evidence only.

## Proof and implementation speed

Production Studio Fast Track governs all coding work: each change must leave the next work better engineered and faster to build.

For Negligible/Small work, use the cheapest credible proof: owning checks, normal validation, changed-source/control-flow inspection, then broader existing checks only as needed. Probes, harnesses, mutation tests, and instrumentation are escalation and count as cost even when deleted. Before adding one, name the unproved fact, why cheaper proof cannot establish it, and why the cost is justified. Use applicable ordinary non-executing validation before temporary executable proof/debugging.

If proof/debugging becomes disproportionate or its machinery needs substantial debugging, stop and reassess before expanding; simplify only when reassessment shows unnecessary cost. Do not re-prove unchanged neighboring invariants with reliable owners. Correct another document only when this change makes a current statement false or incomplete, never by term-matching audit.

## Waits and synchronization

Every operational wait, poll, retry, or synchronization needs a real success condition and deliberate non-success exit; none may trap indefinitely. Prefer observable readiness/progress/failure to elapsed time. When the program can observe that success will not occur without another action, detect that state and stop automatically. Cancellation is backup control, not correction for a detectable stall. Use a narrowly justified failsafe bound only where no credible observable failure/progress signal exists; this is not a blanket timeout policy. Do not use `Sleep` or fixed delay for readiness when a credible observable signal exists; use one only when the delay itself is required or no credible observable replacement exists. Where legitimate work and a stall would otherwise look alike for long periods, expose meaningful waiting/progress/failure status where practical. Long-lived loops, servers, watchers, and observers are not operational waits.

## Correct the owner, not the symptom

Fix a defect at its owner across the defect class; prevent or reliably detect its cause before recovery. Inspect equivalent/sibling paths and deterministic downstream behavior. Retry, fallback, timeout, cancellation, escape, restart, warning, or manual workaround is not the fix when source correction/detection is reasonable. Recovery may be secondary, or the deliberate result only when root correction is impossible, unsupported, or not worth its cost. On failure, keep original information needed to finish manually. Prefer the smallest solution that removes, prevents, or reliably detects the failure, not the smallest patch after it. One local success is not completion evidence.

## Do not treat an intentional workflow result as a failure

When a workflow deliberately stops, closes, reloads, releases a lock, clears temporary state, disconnects, or otherwise causes a state as part of its intended transition, the result itself is not a defect. Do not diagnose it as though something unexpectedly broke, and do not build recovery merely to undo what the workflow intentionally did.

Instead, verify that the intended action actually succeeded and that the workflow can continue from the intended resulting state. If a process was supposed to stop but is still running, a lock was supposed to be released but remains held, a reload never becomes ready, or the workflow fails to reach its required destination, that is a real failure.

Use facts the workflow already established instead of creating duplicate state or re-detecting what the workflow already knows. Do not add crash classification, recovery flags, self-healing, or other detection/recovery machinery solely because an intentional transition resembles a failure state. Legitimate prerequisite checks, refusals, bounded retries, failure handling, and future-compatibility safeguards remain allowed where they independently earn their cost.

This applies both to Production Studio tooling and to workflows inside the products we build.

## Establish the need; reuse existing behavior

Before claiming a gap/need or proposing machinery, inspect only relevant current behavior and closest existing owner/solution to establish a remaining user need. Include accepted human prerequisites, refusals, guards, unsupported cases and simple manual correction. If reading is barred, say unestablished, not missing; if no need, name the mismatch. Before designing/building recovery, retry, salvage, fallback or other machinery, compare a human prerequisite, refusal, correction or fresh normal run. Code recognizing, resuming or finishing prior failed/interrupted work is recovery even on a later manual run; fresh normal execution, guards, refusals and relevant reporting are not. If a human alternative could suffice and Ariel has not specifically approved that machine behavior, stop and raise the concrete choice via ChatGPT; a pasted prompt is not approval.

If need remains, ask both: simplify implementation or remove mechanisms by reordering/reuse? Prefer direct reuse, small refactor, then proven mechanism plus new leaf; partial matches merit reuse.

Build the simplest reliable system for today, while minimizing the cost and fragility of changing it as the tools evolve.

When environment, supported use or scope changes materially, inspect the existing solution before keeping/replacing it. Preserve useful reasoning, decisions, concepts, mechanisms and code; revalidate only affected assumptions and proven scope. Reuse what fits; refactor/generalize what needs adapting; replace/supersede only what no longer fits. Proof covers exercised scope: keep passing stages [OK], untested larger path [Unverified].

Before adding machinery, identify each operation's owner, target, timing, status (designed/implemented/deliberately unsettled) and regression coverage. Prove existing behavior cannot serve before adding a parallel path. Correct caller-only state at caller; change a shared helper for one caller only if its leaf provably cannot work.

## Working or removed

Prove the path or remove it and let code assume correct conditions. Never retain an unverified fallback; Git preserves removed code.

## Durable files contain no one-run state

Do not put run IDs, PIDs, tokens, transfer markers, timestamps, or other one-run values in standing instruction or design files.

## Text encoding and line endings belong to the repository

Repository text, including programmatically written text, is UTF-8 without BOM unless a specific consumer requires a BOM. Decide line endings once in repository policy, normally `.gitattributes`, not per-file exceptions. Byte-for-byte checks normalize endings before comparing/hashing so natural editor, agent, or shell endings do not break them.

## Enumerate before filtering

Enumerate candidates before narrowing a file, window, element, process, or record; do not guess identity first. A destructive debugging or cleanup action against a live process or resource acts only on exact identities established before it runs, never on a name, path, or pattern that could match unrelated live state. Text quoted for later exact matching is an identity too. Before it becomes a literal or edit anchor, verify it against the file's own characters through an exact read rather than terminal-rendered output, and name any nonprinting or control character that affects the match. Rendering aids understanding; it never proves an anchor.

## Trace values through the whole path

Before declaring a value change complete, follow every transform, store, render, control size, and layout step that can affect it.

## Comments describe the current system

Comments state current behavior plus only reason/history needed to understand it. Git owns obsolete history.

## User-visible identifiers name their type

New user-visible identifiers begin with type: `ERR-` failure, `NOTICE-` information, `WARN-` only for a genuinely distinct warning. Subsystem and number follow unchanged. This governs new identifiers only and is not authority to rename existing ones, which records, search terms, and written logs already name.

<!-- BEGIN MARKED SECTION: not synchronized to Codex; Codex reads it on demand -->
## Preserve requirements through design and completion

When materially revising a design, preserve all applicable settled requirements unless the user explicitly supersedes or excludes them. Approval of a revised document changes only the requirements the user explicitly agreed to change; omitted requirements remain binding. Reconcile affected obligations against the accepted design baseline, requirements agreed since that baseline, and subsequent explicit user decisions. Use the affected governing sections' history, not a broad historical audit. Report unresolved removed or weakened obligations before writing or installing the revision.

Before a material Design revision is approved or released for implementation, use its existing discovery, drafting, and independent final review to establish from current source that every materially affected supported action path works through its real callers and helper bodies, **including helpers reused unchanged**. For each changed side effect and removed prerequisite, trace the relevant reads and return conditions through the next consumer to the action or safe refusal. Inspect whether failed reads can silently omit candidates, how uniqueness and identities are established or refound, where the last target/window/page authorization occurs relative to the action, and which shared callers can be affected. Name the necessary guarantee of every removed safeguard and where it is retained, transferred, or explicitly retired. A user's waiver counts only after its evidence-backed consequence for the ordinary supported path and agreed Finished Result has been explained and explicitly accepted. If that path would ordinarily fail to achieve the still-agreed Finished Result, return REVISE rather than treating a waived mechanism as acceptance of a failed outcome; changing the result itself requires the user's explicit reconsideration. Cite source evidence and current bounded provider observations where application behavior materially determines viability; a provider control's identity inferred only from code is not a verified live fact. Distinguish observed, inferred, and unverified claims, and settle consequential evidence gaps before release. When scope or a material decision changes, recheck the newly affected paths rather than treating an earlier inventory or review as covering them. Missing source proof, incompatible helper contracts, unresolved material technical or human decisions, or an ordinary-path/result contradiction mean REVISE and no implementation release. Use the existing investigation, Design and review response; no new tracker, generalized harness, or routine review stage.

Before declaring a journey or independently completable feature finished, reconcile its materially applicable retained requirements with the implementation and credible evidence. In the existing completion report, identify each material requirement or behavioral group, its implementation and affected consumers, the evidence establishing it, and the evidence's scope. Check consequential producer-to-consumer relationships, including relevant states left after failure, interruption, or cancellation and their later use across supported operating contexts. Establish the scope of guards relied upon. Apply the project's detailed revision and completion procedure where one exists.

Credible proof may be mechanical or live under the existing proof requirements. State what it establishes and what remains limited or unfinished. Absence of live acceptance alone does not invalidate adequate machine proof, but any live acceptance required by the agreed completion contract remains outstanding until satisfied. Reporting an unfinished, unsupported, or unproved obligation does not authorize excluding it or declaring the affected feature complete.

Reuse existing design, proof, and completion records. Bound the reconciliation to the affected requirements and consequential interactions. Do not introduce exhaustive historical audits, combinatorial testing, separate tracking artifacts, or extra routine investigation rounds.

## Investigate fully, then challenge and reassess the whole solution

Report every genuine technical finding from a substantive investigation; never narrow discovery to fit an estimate. After the findings, give a distinct Creative alternatives section challenging architecture, assumptions, ownership, operation order, reuse, deletion, refactoring, narrower supported behavior, and human prerequisites/safe refusals. Then give a distinct Whole-solution reassessment: compare the entire accumulated proposal, not only the latest finding, against the original user result for scope drift, overengineering, patch stacks, recovery/retry/fallback, and duplicated responsibilities or proof; state what is removed, reused, and added, and compare equivalent-scope implementation, reliability, and maintenance cost. Repeat this reassessment after each substantial reinvestigation or materially changed review, inside the existing pass rather than a new one. A finding is not an automatic code obligation: keep genuinely necessary safeguards and apply the existing value/authorization gates when proposed scope grows. In staged work, the source-only stage stays source-only; the investigating stage carries the complete analysis, creative alternatives, and whole-solution reassessment together, with no routine added stage. Code quality — robust, maintainable, refactorable, reusable — comes first; speed is secondary.

<!-- END MARKED SECTION -->
